---
title: "event (Справочник по C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords:
- event
- remove
- event_CSharpKeyword
- add
helpviewer_keywords: event keyword [C#]
ms.assetid: 7858fd85-153b-4259-85d0-6aa13c35f174
caps.latest.revision: "28"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: f7e7f9f96714f8988eb91d77c63cc4f017d040f5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="event-c-reference"></a>event (Справочник по C#)
Ключевое слово `event` используется для объявления события в классе Publisher.  
  
## <a name="example"></a>Пример  
 Следующий пример демонстрирует объявление и вызов события, которое использует <xref:System.EventHandler> как базовый тип делегата. Полный пример кода, демонстрирующий использование универсального типа делегата <xref:System.EventHandler%601>, создание подписки на событие и создание метода обработчика событий, см. в разделе [Практическое руководство. Публикация событий, соответствующих рекомендациям .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).  
  
 [!code-csharp[csrefKeywordsModifiers#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/event_1.cs)]  
  
 События представляют собой специальный вид многоадресного делегата, который можно вызвать только из класса или структуры, в которых он объявлен (класс Publisher). Если другие классы или структуры подписываются на событие, их методы обработчиков событий будут вызываться, когда класс Publisher будет вызывать событие. Дополнительные сведения и примеры кода см. в разделах [События](../../../csharp/programming-guide/events/index.md) и [Делегаты](../../../csharp/programming-guide/delegates/index.md).  
  
 События могут быть помечены как [открытый](../../../csharp/language-reference/keywords/public.md), [закрытый](../../../csharp/language-reference/keywords/private.md), [защищенных](../../../csharp/language-reference/keywords/protected.md), [внутренней](../../../csharp/language-reference/keywords/internal.md), [защищенные внутренние](../../../csharp/language-reference/keywords/protected-internal.md) или [private protected](../../../csharp/language-reference/keywords/private-protected.md). Эти модификаторы доступа определяют, каким образом пользователи класса смогут получать доступ к событию. Дополнительные сведения см. в разделе [Модификаторы доступа](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## <a name="keywords-and-events"></a>Ключевые слова и события  
 Следующие ключевые слова применяются к событиям.  
  
|Ключевое слово|Описание|Дополнительные сведения|  
|-------------|-----------------|--------------------------|  
|[static](../../../csharp/language-reference/keywords/static.md)|Делает событие доступным для вызывающих объектов в любое время, даже если экземпляр класса не существует.|[Статические классы и члены статических классов](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)|  
|[virtual](../../../csharp/language-reference/keywords/virtual.md)|Позволяет производным классам переопределять поведение события с помощью ключевого слова [override](../../../csharp/language-reference/keywords/override.md).|[Наследование](../../../csharp/programming-guide/classes-and-structs/inheritance.md)|  
|[sealed](../../../csharp/language-reference/keywords/sealed.md)|Указывает, что для производных классов оно больше не является виртуальным.||  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|Компилятор не будет создавать блоки доступа к событиям `add` и `remove`, и поэтому производные классы должны предоставлять собственную реализацию.||  
  
 Событие может быть объявлено как статическое событие с помощью ключевого слова [static](../../../csharp/language-reference/keywords/static.md). Это делает событие доступным для вызывающих объектов в любое время, даже если экземпляр класса не существует. Дополнительные сведения см. в разделе [Статические классы и члены статических классов](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 Событие может быть помечено как виртуальное событие с помощью ключевого слова [virtual](../../../csharp/language-reference/keywords/virtual.md). Это позволяет производным классам переопределять поведение события с помощью ключевого слова [override](../../../csharp/language-reference/keywords/override.md). Дополнительные сведения см. в разделе [Наследование](../../../csharp/programming-guide/classes-and-structs/inheritance.md). Событие, переопределяющее виртуальное событие, также может быть запечатанным ([sealed](../../../csharp/language-reference/keywords/sealed.md)), что указывает, что для производных классов оно больше не является виртуальным. И наконец, можно объявить событие абстрактным ([abstract](../../../csharp/language-reference/keywords/abstract.md)), что означает, что компилятор не будет создавать блоки доступа к событиям `add` и `remove`. Поэтому производные классы должны предоставлять собственную реализацию.  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Ключевые слова в C#](../../../csharp/language-reference/keywords/index.md)  
 [add](../../../csharp/language-reference/keywords/add.md)  
 [remove](../../../csharp/language-reference/keywords/remove.md)  
 [Модификаторы](../../../csharp/language-reference/keywords/modifiers.md)  
 [Практическое руководство. Объединение делегатов (многоадресные делегаты)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)
