---
title: "Управление параллелизмом с помощью класса DependentTransaction"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ffda721459ef81d148d55359362fe1aeaf9e699e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="managing-concurrency-with-dependenttransaction"></a>Управление параллелизмом с помощью класса DependentTransaction
Объект <xref:System.Transactions.Transaction> создается с помощью метода <xref:System.Transactions.Transaction.DependentClone%2A>. Его единственная цель — гарантировать невозможность фиксации транзакции, пока некоторые фрагменты кода (например рабочий поток) еще выполняют операции над транзакцией. Когда операции в рамках клонированной транзакции завершены и готовы к фиксации, создателю транзакции может быть передано соответствующее уведомление с помощью метода <xref:System.Transactions.DependentTransaction.Complete%2A>. Это позволяет сохранить согласованность и правильность данных.  
  
 Класс <xref:System.Transactions.DependentTransaction> также можно использовать для управления параллелизмом при выполнении асинхронных задач. В этом сценарии родительская транзакция может продолжать выполнение любого кода, пока ее зависимый клон выполняет свои задачи. Другими словами, выполнение родительской транзакции не блокируется до завершения выполнения зависимого клона.  
  
## <a name="creating-a-dependent-clone"></a>Создание зависимого клона  
 Чтобы создать зависимую транзакцию, вызовите метод <xref:System.Transactions.Transaction.DependentClone%2A>, передав ему в качестве параметра перечисление <xref:System.Transactions.DependentCloneOption>. Этот параметр определяет поведение транзакции, когда метод `Commit` родительской транзакции вызывается до того, как зависимый клон указывает, что он готов к фиксации транзакции (путем вызова метода <xref:System.Transactions.DependentTransaction.Complete%2A>). Этот параметр может принимать следующие значения.  
  
-   <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete>. Позволяет создать зависимую транзакцию, блокирующую процесс фиксации родительской транзакции, пока не истечет время ожидания родительской транзакции или пока все зависимые транзакции не вызовут метод <xref:System.Transactions.DependentTransaction.Complete%2A>, указывающий на их завершение. Этот параметр полезно использовать, когда фиксация транзакции должна быть выполнена только после завершения зависимых транзакций. Если родительская транзакция завершает свои операции раньше зависимой транзакции и вызывает метод <xref:System.Transactions.CommittableTransaction.Commit%2A>, процесс фиксации блокируется для выполнения над транзакцией дополнительных операций и создания новых зачислений; блокировка снимается, когда все зависимые транзакции вызовут метод <xref:System.Transactions.DependentTransaction.Complete%2A>. Когда все зависимые транзакции завершат свои операции и вызовут метод <xref:System.Transactions.DependentTransaction.Complete%2A>, начинается процесс фиксации транзакции.  
  
-   <xref:System.Transactions.DependentCloneOption.RollbackIfNotComplete>. Этот параметр, напротив, позволяет создать зависимую транзакцию, которая автоматически прерывается, если метод <xref:System.Transactions.CommittableTransaction.Commit%2A> родительской транзакции вызывается до метода <xref:System.Transactions.DependentTransaction.Complete%2A>. В этом случае все операции зависимой транзакции выполняются как один блок, который нельзя зафиксировать частично.  
  
 Метод <xref:System.Transactions.DependentTransaction.Complete%2A> должен быть вызван только один раз после завершения обработки зависимой транзакции приложением; в противном случае возникает исключение <xref:System.InvalidOperationException>. Попытка выполнить какие-либо дополнительные операции над транзакцией после вызова этого метода приведет к возникновению исключения.  
  
 В следующем примере кода показано, как создать зависимую транзакцию для управления двумя параллельными задачами путем клонирования текущей транзакции и передачи клона рабочему потоку.  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);   
    }  
  
    public void ThreadMethod(object transaction)   
    {   
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);   
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */   
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();   
             dependentTransaction.Dispose();   
        }  
    }  
  
//Client code   
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;      
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
```  
  
 Клиентский код создает область транзакции, которая также задает внешнюю транзакцию. Не следует передавать внешнюю транзакцию рабочему потоку. Вместо этого следует клонировать текущую (внешнюю) транзакцию путем вызова метода <xref:System.Transactions.Transaction.DependentClone%2A> для текущей транзакции и передачи зависимой транзакции рабочему потоку.  
  
 Метод `ThreadMethod` выполняется в новом потоке. Клиентский код запускает новый поток, передавая зависимую транзакцию в качестве параметра `ThreadMethod`.  
  
 Поскольку зависимая транзакция создается с параметром <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete>, исходная транзакция может быть зафиксирована только после завершения всех операций во втором потоке и вызова метода <xref:System.Transactions.DependentTransaction.Complete%2A> зависимой транзакции. Это означает, что если заканчивается области клиента (при попытке удалить объект транзакции в конце **с помощью** инструкции) перед новый поток вызывает метод <xref:System.Transactions.DependentTransaction.Complete%2A> на зависимая транзакция блокирует код клиента до <xref:System.Transactions.DependentTransaction.Complete%2A> вызывается для зависимого. После этого может быть завершен процесс фиксации или прерывания транзакции.  
  
## <a name="concurrency-issues"></a>Проблемы параллелизма  
 При использовании класса <xref:System.Transactions.DependentTransaction> следует помнить о нескольких дополнительных проблемах параллелизма.  
  
-   Если рабочий поток откатывает транзакцию, а родительская транзакция пытается ее зафиксировать, возникает исключение <xref:System.Transactions.TransactionAbortedException>.  
  
-   Для каждого рабочего потока в транзакции следует создавать новый зависимый клон. Не следует передавать один и тот же зависимый клон нескольким потокам, поскольку только один из них может вызвать метод <xref:System.Transactions.DependentTransaction.Complete%2A> зависимого клона.  
  
-   Если рабочий поток порождает новый рабочий поток, следует создать новый зависимый клон из существующего зависимого клона и передать его новому потоку.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Transactions.DependentTransaction>
