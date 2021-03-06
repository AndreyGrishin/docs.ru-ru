---
title: "Практическое руководство. Добавление элементов меню в элемент управления ContextMenuStrip"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ContextMenuStrips [Windows Forms], adding menu items
- shortcut menus [Windows Forms], adding items
- context menus [Windows Forms], adding menu items
ms.assetid: 1ec14776-3ea2-4752-bd22-4fae0fd19e1a
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b64cab6815b408b438d5ca93c3c7166aa940bf67
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-add-menu-items-to-a-contextmenustrip"></a>Практическое руководство. Добавление элементов меню в элемент управления ContextMenuStrip
Можно добавить только один элемент меню или несколько элементов одновременно, чтобы <xref:System.Windows.Forms.ContextMenuStrip>.  
  
### <a name="to-add-a-single-menu-item-to-a-contextmenustrip"></a>Чтобы добавить отдельный элемент меню в элемент управления ContextMenuStrip  
  
-   Используйте <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> метод для добавления одного пункта меню <xref:System.Windows.Forms.ContextMenuStrip>.  
  
    ```vb  
    Me.contextMenuStrip1.Items.Add(Me.toolStripMenuItem1)  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.Add(toolStripMenuItem1);  
    ```  
  
### <a name="to-add-several-menu-items-to-a-contextmenustrip"></a>Чтобы добавить несколько элементов меню в элемент управления ContextMenuStrip  
  
-   Используйте <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> метод для добавления нескольких пунктов меню <xref:System.Windows.Forms.ContextMenuStrip>.  
  
    ```vb  
    Me.contextMenuStrip1.Items.AddRange(New _  
       System.Windows.Forms.ToolStripItem() {Me.toolStripMenuItem1, _  
          Me.toolStripMenuItem2})  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.AddRange(new   
       System.Windows.Forms.ToolStripItem[] {  
          this.toolStripMenuItem1, this.toolStripMenuItem2});  
    ```  
  
## <a name="see-also"></a>См. также  
 [Элемент управления ContextMenuStrip](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)
