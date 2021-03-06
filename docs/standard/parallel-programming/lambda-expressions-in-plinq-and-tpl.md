---
title: "Лямбда-выражения в PLINQ и библиотеке параллельных задач"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Func delegate, creating with lambda expression
- Action delegate, creating with lambda expression
- lambda expressions, with Action and Func
ms.assetid: 645b2c17-29d0-4ffa-8684-430743cc2f2d
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 79ab0f4427e0f37259f88cd3ec0762d1582481f1
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="lambda-expressions-in-plinq-and-tpl"></a>Лямбда-выражения в PLINQ и библиотеке параллельных задач
Библиотека параллельных задач (TPL) содержит множество методов, которые принимают одно из <xref:System.Func%601?displayProperty=nameWithType> или <xref:System.Action?displayProperty=nameWithType> семейства делегатов в качестве входных параметров. Используйте эти делегаты для передачи пользовательской программной логики в параллельный цикл, задачу или запрос. В примерах кода для библиотеки параллельных задач и PLINQ лямбда-выражения используются для создания экземпляров этих делегатов как встроенных блоков кода. В этом разделе дается краткое введение в делегаты Func и Action и демонстрируется использование лямбда-выражений в библиотеке параллельных задач и PLINQ.  
  
 **Примечание.** Дополнительные сведения о делегатах см. в разделах [Делегаты](../../csharp/programming-guide/delegates/index.md) и [Делегаты](../../visual-basic/programming-guide/language-features/delegates/index.md). Дополнительные сведения о лямбда-выражениях в C# и [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] см. в разделах [Лямбда-выражения](~/docs/csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) и [Лямбда-выражения](~/docs/visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
## <a name="func-delegate"></a>Делегат Func  
 Делегат `Func` инкапсулирует метод, который возвращает значение. В сигнатуре Func последний или крайний правый тип параметра всегда указывает возвращаемый тип. Распространенная причина возникновения ошибки компилятора — попытка передать два входных параметра в <xref:System.Func%602?displayProperty=nameWithType>; на самом деле этот тип принимает только один входной параметр. Библиотека классов Framework определено 17 версий `Func`: <xref:System.Func%601?displayProperty=nameWithType>, <xref:System.Func%602?displayProperty=nameWithType>, <xref:System.Func%603?displayProperty=nameWithType>, и так далее до через <xref:System.Func%6017?displayProperty=nameWithType>.  
  
## <a name="action-delegate"></a>Делегат Action  
 Объект <xref:System.Action?displayProperty=nameWithType> делегат инкапсулирует метод (Sub в [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]), не возвращает значение, или возвращает [void](~/docs/csharp/language-reference/keywords/void.md). В сигнатуре типа Action параметры типа представляют только входные параметры. Как и в случае с делегатом Func, библиотека классов Framework определяет 17 версий делегата Action, начиная с версии без параметров типа и заканчивая версией с 16 параметрами типа.  
  
## <a name="example"></a>Пример  
 В следующем примере для <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=nameWithType> метод демонстрируется express делегатах Func и Action с помощью лямбда-выражения.  
  
 [!code-csharp[System.Threading.Tasks.Parallel#02](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.threading.tasks.parallel/cs/parallelforeach.cs#02)]
 [!code-vb[System.Threading.Tasks.Parallel#02](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.threading.tasks.parallel/vb/parallelforeach.vb#02)]  
  
## <a name="see-also"></a>См. также  
 [Параллельное программирование](../../../docs/standard/parallel-programming/index.md)
