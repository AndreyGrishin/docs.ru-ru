---
title: "Ограничения (F#)"
description: "Дополнительные сведения об ограничениях F #, которые применяются для параметров универсального типа для задания требований к аргументу типа в универсальном типе или функции."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 2f232a3a-9486-48fb-9759-f23404ed4b52
ms.openlocfilehash: 91854fd2f692688e0f1c27aba1422eff64156048
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="constraints"></a>Ограничения

В этом разделе описываются ограничения, которые можно применить к универсальным параметрам типа для укажите требования для аргумента типа в универсальном типе или функции.


## <a name="syntax"></a>Синтаксис

```fsharp
type-parameter-list when constraint1 [ and constraint2]
```

## <a name="remarks"></a>Примечания
Существует несколько различных ограничений, которые можно применять для ограничения типов, которые могут использоваться в универсальном типе. В следующей таблице перечислены и описаны эти ограничения.

|Ограничение|Синтаксис|Описание|
|----------|------|-----------|
|Ограничения типа|*параметр типа* :&gt; *типа*|Переданный тип должен быть равен или быть производным от типа, указанного или, если тип является интерфейсом, переданный тип должен реализовывать интерфейс.|
|Ограничение NULL|*параметр типа* : значение null|Переданный тип должен поддерживать литералом null. Сюда входят все типы .NET объектов, но не F # список, кортеж, функции, класса, записи или типы объединений.|
|Ограничение явных членов|[()]*параметр типа* [или... или *параметр типа*)]: (* сигнатура элемента *)|Хотя бы один из передаваемых методу аргументов типа должен иметь член, имеющий заданную сигнатуру; не предназначен для широкого использования. Члены должны быть либо явно определены на быть допустимых целевых объектов для явное ограничение член типа или часть неявный тип расширения.|
|Ограничение конструктора|*параметр типа* : (new: единицы -&gt; ")|Переданный тип должен иметь конструктор по умолчанию.|
|Ограничение типа значения|: структура|Переданный тип должен быть типом значения .NET.|
|Ограничение ссылочного типа|: не структуры|Переданный тип должен быть ссылочным типом .NET.|
|Ограничение типа перечисления|: перечисление&lt;*базовый тип*&gt;|Переданный тип должен быть перечислимый тип с помощью заданного базового типа. не предназначен для широкого использования.|
|Ограничение по делегату|: делегировать&lt;*параметра типа кортежа*, *типа возвращаемого значения*&gt;|Предоставленный тип должен быть тип делегата, который имеет указанные аргументы и возвращаемое значение; не предназначен для широкого использования.|
|Ограничение по сравнению|: сравнение|Переданный тип должен поддерживать сравнение.|
|Ограничение равенства|: равенства|Переданный тип должен поддерживать равенство.|
|Неуправляемые ограничения|: неуправляемые|Переданный тип должен быть неуправляемого типа. Неуправляемые типы являются некоторых простых типов (`sbyte`, `byte`, `char`, `nativeint`, `unativeint`, `float32`, `float`, `int16`, `uint16`, `int32`, `uint32`, `int64`, `uint64`, или `decimal`), типы перечисления `nativeptr&lt;_&gt;`, или не являющимися универсальными структуры, поля которого являются все неуправляемые типы.|
Необходимо добавить ограничение, когда нужно использовать функцию, которая доступна на тип ограничения, но не для типов в общем коде. Например при использовании ограничение типа для указания типа класса можно использовать один из методов этого класса в универсальной функции или типа.

Указание ограничений иногда является необходимым при написании параметры типа явно, так как без ограничения, компилятор не может проверить, что компоненты, которые вы используете будут доступны на любой тип, который может быть передан во время выполнения для типа параметр.

Наиболее распространенные ограничения, которые использовать в коде F # — это ограничения типа, которые задают базовые классы или интерфейсы. Другие ограничения используются в библиотеке F # для реализации определенных функций, таких как ограничения явных членов, которое используется для реализации перегрузки операторов для арифметических операторов, или потому, что F # поддерживает полный предоставляются набор ограничений, поддерживаемый средой CLR.

В процессе определения типа некоторые ограничения автоматически выводятся компилятором. Например, если вы используете `+` оператор в функции, компилятор выводит явных членов ограничения на типы переменных, которые используются в выражении.

Следующий код иллюстрирует объявления некоторых ограничений.

```fsharp
// Base Type Constraint
type Class1<'T when 'T :> System.Exception> =
class end

// Interface Type Constraint
type Class2<'T when 'T :> System.IComparable> = 
class end

// Null constraint
type Class3<'T when 'T : null> =
class end

// Member constraint with static member
type Class4<'T when 'T : (static member staticMethod1 : unit -> 'T) > =
class end

// Member constraint with instance member
type Class5<'T when 'T : (member Method1 : 'T -> int)> =
class end

// Member constraint with property
type Class6<'T when 'T : (member Property1 : int)> =
class end

// Constructor constraint
type Class7<'T when 'T : (new : unit -> 'T)>() =
member val Field = new 'T()

// Reference type constraint
type Class8<'T when 'T : not struct> =
class end

// Enumeration constraint with underlying value specified
type Class9<'T when 'T : enum<uint32>> =
class end

// 'T must implement IComparable, or be an array type with comparable
// elements, or be System.IntPtr or System.UIntPtr. Also, 'T must not have
// the NoComparison attribute.
type Class10<'T when 'T : comparison> =
class end

// 'T must support equality. This is true for any type that does not
// have the NoEquality attribute.
type Class11<'T when 'T : equality> =
class end

type Class12<'T when 'T : delegate<obj * System.EventArgs, unit>> =
class end

type Class13<'T when 'T : unmanaged> =
class end

// Member constraints with two type parameters
// Most often used with static type parameters in inline functions
let inline add(value1 : ^T when ^T : (static member (+) : ^T * ^T -> ^T), value2: ^T) =
value1 + value2

// ^T and ^U must support operator +
let inline heterogenousAdd(value1 : ^T when (^T or ^U) : (static member (+) : ^T * ^U -> ^T), value2 : ^U) =
value1 + value2

// If there are multiple constraints, use the and keyword to separate them.
type Class14<'T,'U when 'T : equality and 'U : equality> =
class end
```

## <a name="see-also"></a>См. также
[Универсальные шаблоны](index.md)

[Ограничения](constraints.md)
