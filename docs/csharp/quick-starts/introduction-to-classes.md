---
title: "Краткие руководства | Общие сведения о классах | Руководство по C#"
description: "Создайте свою первую программу на C# и ознакомьтесь с основными понятиями объектно-ориентированного программирования"
author: billwagner
ms.author: wiwagn
ms.date: 10/11/2017
ms.topic: get-started-article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 4e15b1b12b9420ca1781eca3f2578fa24c9ec82a
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2018
---
# <a name="introduction-to-classes"></a>Общие сведения о классах

Для работы с этим кратким руководством вам потребуется компьютер, который можно использовать для разработки. В руководстве по [началу работы с .NET за 10 минут](https://www.microsoft.com/net/core) содержатся инструкции по настройке локальной среды разработки на компьютерах Mac, Windows или Linux. Краткий обзор команд, которые будут использоваться, и ссылки на дополнительные сведения представлены в [вводной статье к руководствам по локальным средам](local-environment.md).

## <a name="create-your-application"></a>Создание приложения

С помощью окна терминала создайте каталог с именем **classes**. В этом каталоге вы создадите приложение. Откройте этот каталог и введите в окне консоли `dotnet new console`. При помощи этой команды создается приложение. Откройте файл **Program.cs**. Он должен выглядеть так:

```csharp
using System;

namespace classes
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

С помощью этого краткого руководства вы создадите новые типы, представляющие банковский счет. Обычно разработчики определяют каждый класс в отдельном текстовом файле. Благодаря этому программой легче управлять, когда ее размер увеличивается.  Создайте новый файл с именем **BankAccount.cs** в каталоге **classes**. 

Этот файл будет содержать определение ***банковского счета***. Средства объектно-ориентированного программирования обеспечивают упорядочение кода. При этом создаются типы в виде ***классов***. Классы содержат код, который представляет отдельную сущность. Класс `BankAccount` представляет банковский счет. Этот код реализует определенные операции с помощью методов и свойств. В этом кратком руководстве банковский счет поддерживает следующий режим работы:

1. Представляет собой число из 10 цифр, которое однозначно определяет банковский счет.
1. Содержит строку, в которой хранятся имена владельцев.
1. Позволяет получить данные сальдо.
1. Принимает депозиты.
1. Принимает списания.
1. Начальное сальдо должно было положительным.
1. После списания не должно оставаться отрицательное сальдо.

## <a name="define-the-bank-account-type"></a>Определение типа банковского счета

Сначала можно создать основы класса, который определяет такой режим работы. Он должен выглядеть так:

```csharp
using System;

namespace classes
{
    public class BankAccount
    {
        public string Number { get; }
        public string Owner { get; set; }
        public decimal Balance { get; }

        public void MakeDeposit(decimal amount, DateTime date, string note)
        {
        }

        public void MakeWithdrawal(decimal amount, DateTime date, string note)
        {
        }
    }
}
```

Прежде чем продолжить, рассмотрим созданный код.  Объявление `namespace` предоставляет способ логического упорядочения кода. Это относительно небольшое руководство, поэтому весь код будет находиться в одном пространстве имен. 

`public class BankAccount` определяет класс или тип, который вы создаете. Весь код в скобках `{` и `}`, который следует за объявлением класса, определяет поведение класса. Есть пять ***элементов*** класса `BankAccount`. Первые три элемента представляют собой ***свойства***. Свойства являются элементами данных и могут содержать код для запуска проверки или других правил. Последние два элемента являются ***методами***. Методы представляют собой блоки кода, которые выполняют только одну функцию. Имя каждого элемента должно содержать достаточно информации, чтобы разработчик мог понять, какие функции выполняет класс.

## <a name="open-a-new-account"></a>Открытие нового счета

Сначала нужно открыть банковский счет. Когда клиент открывает счет, он должен указать начальное сальдо и сведения о владельцах этого счета. 

Создайте новый объект типа `BankAccount`, чтобы определить ***конструктор***, который назначает эти значения. ***Конструктор*** — это элемент, имя которого совпадает с классом. Он используется для инициализации объектов этого типа класса. Добавьте следующий конструктор в тип `BankAccount`:

```csharp
public BankAccount(string name, decimal initialBalance)
{
    this.Owner = name;
    this.Balance = initialBalance;
}
```

Конструкторы вызываются при создании объекта с помощью [`new`](../language-reference/keywords/new.md). Замените строку `Console.WriteLine("Hello World!");` в файле ***program.cs*** следующей строкой (замените `<name>` своим именем):

```csharp
var account = new BankAccount("<name>", 1000);
Console.WriteLine($"Account {account.Number} was created for {account.Owner} with {account.Balance} initial balance.");
```

Введите `dotnet run`, чтобы просмотреть результаты.  

Вы заметили, что номер счета не указан? Нужно решить эту проблему. Номер счета следует назначить при создании объекта. Но создавать этот номер не входит в обязанности вызывающего. Код класса `BankAccount` должен иметь информацию о том, как присвоить номера новым счетам.  Проще всего начать с 10-значного числа. Увеличивайте его при создании каждого нового счета. Затем при создании объекта сохраните номер текущего счета.

Добавьте в класс `BankAccount` следующее объявление элемента:

```csharp
private static int accountNumberSeed = 1234567890;
```

Это элемент данных. Он имеет свойство `private`, то есть к нему может получить доступ только код внутри класса `BankAccount`. Таким образом общедоступные обязательства (например, получение номера счета) отделяются от закрытой реализации (способ создания номеров счетов). Добавьте две следующие строки в конструктор, чтобы назначить номер счета:

```csharp
this.Number = accountNumberSeed.ToString();
accountNumberSeed++;
```

Введите `dotnet run`, чтобы просмотреть результаты.

## <a name="create-deposits-and-withdrawals"></a>Создание депозитов и списаний

Для надлежащей работы ваш класс банковского счета должен принимать депозиты и списания. Чтобы реализовать депозиты и списания, создадим журнал для каждой транзакции на счете. Этот подход предпочтительнее, чем простое обновление сальдо после каждой транзакции. Журнал можно использовать для аудита всех транзакций и управления ежедневным сальдо. При необходимости можно вычислять сальдо с помощью журнала всех транзакций. Тогда при следующем вычислении все исправленные ошибки в одной транзакции будут правильно учтены в сальдо.

Начнем с создания нового типа, который представляет транзакцию. Это простой тип без обязательств. Ему нужно назначить несколько свойств. Создайте новый файл с именем ***Transaction.cs***. Добавьте в этот файл следующий код:

[!code-csharp[Transaction](../../../samples/csharp/classes-quickstart/Transaction.cs "Transaction declaration")]

Теперь добавим <xref:System.Collections.Generic.List%601> объектов `Transaction` в класс `BankAccount`. Добавьте следующее объявление:

[!code-csharp[TransactionDecl](../../../samples/csharp/classes-quickstart/BankAccount.cs#TransactionDeclaration "Transaction declaration")]

Класс <xref:System.Collections.Generic.List%601> требует импортировать другое пространство имен. Добавьте следующий код в начало файла **BankAccount.cs**:

```csharp
using System.Collections.Generic;
```

Теперь изменим способ отчета `Balance`.  Чтобы вычислить его, нужно суммировать значения всех транзакций. Измените объявление `Balance` в классе `BankAccount` следующим образом:

[!code-csharp[BalanceComputation](../../../samples/csharp/classes-quickstart/BankAccount.cs#BalanceComputation "Computing the balance")]

В этом примере показан важный аспект ***свойств***. Вы вычисляете сальдо, когда другой программист запрашивает значение. В результате вашего вычисления выводится список всех транзакций и сумма в виде текущего сальдо.

Теперь реализуйте методы `MakeDeposit` и `MakeWithdrawal`. Эти методы будут выполнять два последних правила: начальное сальдо должно быть положительным, списание не должно создавать отрицательное сальдо. 

Это действие вводит понятие ***исключений***. Чтобы определить, что метод не может выполнить свою функцию, обычно вызывается исключение. В типе исключения и связанном с ним сообщении описывается ошибка. В этом примере метод `MakeDeposit` вызывает исключение, если сумма депозита является отрицательной. Метод `MakeWithdrawal` вызывает исключение, если сумма списания является отрицательной или если при применении списания создается отрицательное сальдо:

[!code-csharp[DepositAndWithdrawal](../../../samples/csharp/classes-quickstart/BankAccount.cs#DepositAndWithdrawal "Make deposits and withdrawals")]

Инструкция [`throw`](../language-reference/keywords/throw.md) **вызывает** исключение. Когда будет найден соответствующий блок `catch`, выполнение текущего метода завершится и возобновится. Вы добавите блок `catch` для тестирования этого кода немного позже.

Чтобы вместо непосредственного обновления сальдо добавлялась начальная транзакция, конструктор должен получить одно изменение. Так как вы уже написали метод `MakeDeposit`, вызовите его из конструктора. Готовый конструктор должен выглядеть так:

[!code-csharp[Constructor](../../../samples/csharp/classes-quickstart/BankAccount.cs#Constructor "The final version of the constructor")]

<xref:System.DateTime.Now?displayProperty=nameWithType> — это свойство, которое возвращает текущие дату и время. Протестируйте его, добавив несколько депозитов и списаний в метод `Main`:

```csharp
account.MakeWithdrawal(500, DateTime.Now, "Rent payment");
Console.WriteLine(account.Balance);
account.MakeDeposit(100, DateTime.Now, "friend paid me back");
Console.WriteLine(account.Balance);
```

Теперь протестируйте обнаружение условий ошибки. Для этого создайте счет с отрицательным сальдо:

```csharp
// Test that the initial balances must be positive:
try
{
    var invalidAccount = new BankAccount("invalid", -55);
}
catch (ArgumentOutOfRangeException e)
{
    Console.WriteLine("Exception caught creating account with negative balance");
    Console.WriteLine(e.ToString());
}
```

С помощью [`try` и `catch` инструкций](../language-reference/keywords/try-catch.md) пометьте блок кода, который может вызывать исключения и обнаруживать потенциальные ошибки. Таким же образом можно протестировать код, который вызывает исключение в случае создания отрицательного сальдо:

```csharp
// Test for a negative balance
try
{
    account.MakeWithdrawal(750, DateTime.Now, "Attempt to overdraw");
}
catch (InvalidOperationException e)
{
    Console.WriteLine("Exception caught trying to overdraw");
    Console.WriteLine(e.ToString());
}
```

Сохраните файл и введите `dotnet run` для проверки.

## <a name="challenge---log-all-transactions"></a>Задача — регистрация всех транзакций

Чтобы завершить работу с этим кратким руководством, можно написать метод `GetAccountHistory`, который создает `string` для журнала транзакций. Добавьте этот метод в тип `BankAccount`:

[!code-csharp[History](../../../samples/csharp/classes-quickstart/BankAccount.cs#History "Display transaction history")]

В этом примере используется класс <xref:System.Text.StringBuilder>, чтобы отформатировать строку, которая содержит одну строку для каждой транзакции. Код форматирования строки приведен выше в этом руководстве. В этом коде есть новый символ `\t`. Он позволяет вставить вкладку для форматирования выходных данных.

Добавьте следующую строку, чтобы проверить его в файле **Program.cs**:

```csharp
Console.WriteLine(account.GetAccountHistory());
```

Введите `dotnet run`, чтобы просмотреть результаты.

## <a name="next-steps"></a>Следующие шаги

Если у вас возникли вопросы, см. оригинал этого руководства [в нашем репозитории GitHub](https://github.com/dotnet/docs/tree/master/samples/csharp/classes-quickstart/).

Поздравляем! Вы выполнили задачи всех наших кратких руководств. Если вы хотите узнать больше, обратитесь к нашим [руководствам](../tutorials/index.md).
