---
title: "Общие сведения об элементе управления Label (Windows Forms)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: Label
helpviewer_keywords:
- images [Windows Forms], displaying in labels
- labels
- Label control [Windows Forms], about Label control
ms.assetid: dcad7f44-11b7-4c55-b0c0-d984ade43d7d
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f68642eb5f996722097976e042006afbf366ae39
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="label-control-overview-windows-forms"></a>Общие сведения об элементе управления Label (Windows Forms)
Windows Forms <xref:System.Windows.Forms.Label> элементы управления используются для отображения текста или изображений, которые не может быть изменена пользователем. Они используются для идентификации объектов в форме — для предоставления описание какие определенный элемент управления будет выполнять при щелчке, например или для отображения сведений в ответ на событие во время выполнения или процесса в приложении. Например метки можно использовать для добавления описательных заголовков в текстовые поля, списки, поля со списком и т. д. Также можно написать код, который изменяет текст, отображаемый в метке в ответ на события во время выполнения. Например если приложение использует несколько минут, чтобы обрабатывать изменения, можно отобразить сообщение о состоянии обработки в метке.  
  
## <a name="working-with-the-label-control"></a>Работа с элементом управления Label  
 Поскольку <xref:System.Windows.Forms.Label> управления не может получать фокус, он может также использоваться для создания клавиш доступа для других элементов управления. Клавиша доступа позволяет пользователю выбрать другой элемент управления, нажав клавишу ALT, с помощью ключа доступа. Дополнительные сведения см. в разделе [Создание сочетаний клавиш для элементов управления Windows Forms](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md) и [как: создать клавиши доступа, с помощью элементов управления Windows Forms метка](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md).  
  
 Заголовок, отображаемый в метке содержится в <xref:System.Windows.Forms.Label.Text%2A> свойство. <xref:System.Windows.Forms.Label.TextAlign%2A> Свойство позволяет задать выравнивание текста в метке. Дополнительные сведения см. в разделе [как: значение текста, отображаемого элементом управления Windows Forms](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.Label>  
 [Практическое руководство. Приведение размера элемента управления Label в соответствие с его содержимым в Windows Forms](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)  
 [Практическое руководство. Определение клавиш доступа с помощью элементов управления Label в Windows Forms](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md)
