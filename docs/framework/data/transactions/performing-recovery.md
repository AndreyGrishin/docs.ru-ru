---
title: "Выполнение восстановления"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6dd17bf6-ba42-460a-a44b-8046f52b10d0
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 3a215a7f516c2a3f0173b2ebfbd1c52911dee654
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="performing-recovery"></a>Выполнение восстановления
Диспетчер ресурсов обеспечивает разрешение зачислений устойчивых ресурсов в транзакции, повторно зачисляя участника транзакции после сбоя ресурса.  
  
## <a name="the-recovery-process"></a>Процесс восстановления  
 Для зачисления устойчивого ресурса (описываемого реализацией интерфейса <xref:System.Transactions.IEnlistmentNotification>), который способен к восстановлению, необходимо вызвать метод <xref:System.Transactions.Transaction.EnlistDurable%2A>. Кроме того, необходимо предоставить метод <xref:System.Transactions.Transaction.EnlistDurable%2A> с идентификатором диспетчера ресурсов (<xref:System.Guid>), который используется для постоянной отметки участника транзакции в событии сбоя ресурса. По этой причине <xref:System.Guid> , предоставляется для начальной Enlist вызов должен быть идентичен *resourceManagerIdentifier* параметр в <xref:System.Transactions.TransactionManager.Reenlist%2A> вызова во время восстановления. В противном случае возникает исключение <xref:System.Transactions.TransactionException>. Дополнительные сведения о долговременным присоединением к транзакции. в разделе [прикрепление ресурсов в качестве участников в транзакции](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md) .  
  
 Если в фазе подготовки (фазе 1) протокола двухфазной фиксации пользовательская реализация диспетчера ресурсов получает уведомление <xref:System.Transactions.IEnlistmentNotification.Prepare%2A>, она должна создать запись о подготовке в журнале. Запись должна включать всю необходимую информацию для завершения транзакции фиксацией. Подготовка записи позже могут быть доступны при восстановления путем извлечения <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> свойство *preparingEnlistment* обратного вызова. Создание этой записи в рамках метода <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> не требуется, поскольку диспетчер ресурсов может сделать это в рабочем потоке.  
  
 Процесс восстановления состоит из следующих двух шагов.  
  
### <a name="step-1---reenlist"></a>Шаг 1 - повторное зачисление  
 Диспетчер ресурсов проверяет запись о подготовке для каждого зачисления, которое находится под сомнением. Это выполняется путем проверки свойства <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> обратного вызова <xref:System.Transactions.PreparingEnlistment>, переданного диспетчеру ресурсов в уведомлении <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> в фазе 1.  
  
 Для каждого проверяемого зачисления диспетчер ресурсов вызывает метод <xref:System.Transactions.TransactionManager.Reenlist%2A> для диспетчера транзакций. Этот метод передает уникальный <xref:System.Guid>, идентифицирующий диспетчер ресурсов, а также данные перечисления в массиве байтов. Возвращается новый объект <xref:System.Transactions.Enlistment>. Если в результате повторного зачисления возникает исключение, диспетчеру необходимо повторить попытку через некоторое время.  
  
 Метод <xref:System.Transactions.TransactionManager.Reenlist%2A> следует вызывать только после перезапуска диспетчера ресурсов после сбоя. Кроме того, повторное зачисление следует выполнить только для неразрешенных транзакций, зарегистрированных диспетчером ресурсов в ходе начальной фазы подготовки двухфазной фиксации. Любая попытка вызова этого метода в недопустимое время может привести к ошибочным результатам.  
  
 При повторном зачислении участника с помощью этого метода в зависимости от результата транзакции вызывается соответствующий метод фазы 2 интерфейса <xref:System.Transactions.IEnlistmentNotification> (<xref:System.Transactions.IEnlistmentNotification.Commit%2A>, <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> или <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A>).  
  
### <a name="step-2---completing-the-recovery"></a>Шаг 2 - завершение восстановления  
 После завершения всех повторных зачислений диспетчер транзакций вызывает метод <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>. Этот метод завершает восстановление и информирует диспетчер транзакций о том, что у диспетчера ресурсов больше нет транзакций, находящихся под сомнением. Это позволяет гарантировать, что диспетчер ресурсов не вызовет метод <xref:System.Transactions.TransactionManager.Reenlist%2A> повторно.  
  
 От диспетчера ресурсов не требуется разрешения всех транзакций, находящихся по сомнением, перед повторным зачислением в новые транзакции. Сначала можно выполнить в любое время после диспетчера ресурсов устанавливает связь с диспетчером транзакций, но после <xref:System.Transactions.TransactionManager.RecoveryComplete%2A> был вызван (шаг 2); шаг 1 не может выполняться снова. Шаг 2 можно выполнить несколько раз без воздействия на результат транзакций.
