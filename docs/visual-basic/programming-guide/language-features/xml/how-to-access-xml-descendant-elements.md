---
title: "Практическое руководство. Доступ к производным XML элементам (Visual Basic)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML descendent axis property [Visual Basic]
- XML axis [Visual Basic], descendent
- descendent axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: aabfa258-4112-4e7e-bab9-403f96072ef7
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 7b3b6c8ac96bd18a379804b83f3ab3e48a5b0c89
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-access-xml-descendant-elements-visual-basic"></a>Практическое руководство. Доступ к производным XML элементам (Visual Basic)
В этом примере показано, как использовать свойство дочерней оси для доступа ко всем элементам XML, с указанным именем, содержащиеся в XML-элемента. В частности, он использует `Value` свойство, чтобы получить значение первого элемента в коллекции, `name` возвращает свойство дочерней оси. `name` Свойство дочерней оси возвращает все элементы с именем `name` , содержащихся в `contacts` объекта. В этом примере также используется `phone` свойство дочерней оси для доступа ко всем потомкам с именем `phone` , содержащихся в `contacts` объекта.  
  
## <a name="example"></a>Пример  
 [!code-vb[VbXMLSamples#31](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-access-xml-descendant-elements_1.vb)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Для этого примера требуются:  
  
-   ссылка на пространство имен <xref:System.Xml.Linq>.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType>  
 [Свойство дочерней оси XML](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)  
 [Свойство значения XML](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)  
 [Доступ к XML в Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
