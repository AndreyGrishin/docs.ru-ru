---
title: "UI Automation Support for the Header Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, Header control type"
  - "Header control type"
  - "control types, Header"
ms.assetid: d2e48891-2dbe-409e-8655-2f753908e29b
caps.latest.revision: 20
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 20
---
# UI Automation Support for the Header Control Type
> [!NOTE]
>  Эта документация предназначена для разработчиков .NET Framework, желающих использовать управляемые классы [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], заданные в пространстве имен <xref:System.Windows.Automation>. Последние сведения о [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] см. в разделе [API автоматизации Windows. Автоматизация пользовательского интерфейса](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 В этом разделе содержатся сведения о поддержке [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] типа элемента управления Header. В [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] тип элемента управления — это набор условий, которым должен удовлетворять элемент управления для использования свойства <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Эти условия включают определенные правила для древовидной структуры [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], шаблонов элементов управления и значений свойств [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
 Элемент управления "Заголовок" предоставляет визуальный контейнер для меток строк или столбцов данных.  
  
 В следующих разделах описывается необходимая древовидная структура [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], свойства, шаблоны элементов управления и события для типа элемента управления Header. Требования [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] применяются ко всем элементам управления "Заголовок", будь это [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] или [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Требуемая древовидная структура модели автоматизации пользовательского интерфейса  
 В следующей таблице описывается представление элемента управления и представление содержимого дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], относящиеся к элементам управления "Заголовок", и показывается, что может содержаться в каждом представлении. Дополнительные сведения о дереве [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] см. в разделе [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Представление элемента управления|Представление содержимого|  
|---------------------------------------|-------------------------------|  
|Header<br /><br /> -   HeaderItem \(1 или более\)|Нет|  
  
 Элементы управления "Заголовок" всегда имеют 1 или более дочерних элементов в представлении элемента управления дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]  
  
 Элементы управления "Заголовок" не имеют дочерних элементов в представлении содержимого дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]  
  
<a name="Required_UI_Automation_Properties"></a>   
## Требуемые свойства модели автоматизации пользовательского интерфейса  
 В следующей таблице перечислены свойства [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], значения или определения которых особенно актуальны для элементов управления "Заголовок". Дополнительные сведения о свойствах [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] см. в разделе [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Свойство [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|Значение|Примечания|  
|-------------------------------------------------------------------------------------|--------------|----------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|См. примечания.|Значение этого свойства должно быть уникальным среди всех элементов управления в приложении.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|См. примечания.|Внешний прямоугольник, содержащий весь элемент управления.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|См. примечания.|Поддерживается при наличии ограничивающего прямоугольника. Если не все точки внутри ограничивающего прямоугольника являются интерактивными и выполняется специализированная проверка на наличие данных, выполните переопределение и предоставьте интерактивную точку.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|См. примечания.|Если элемент управления может получать фокус клавиатуры, он должен поддерживать это свойство.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|См. примечания.|Элемент управления "Заголовок" должен иметь имя, если существует несколько заголовков строк или несколько заголовков столбцов. Оно определяет сведения в заголовке.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`.|Элементы управления "Заголовок" не имеют меток со статическим текстом.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Header|Это значение является одинаковым для всех инфраструктур [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"заголовок"|Это значение является одинаковым для всех инфраструктур [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.OrientationProperty>|Горизонтально|Значение этого свойства представляет положение элемента управления "Заголовок", является ли он заголовком строки или столбца.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|Элемент управления "Заголовок" не включается в представление содержимого дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Элемент управления "Заголовок" всегда включается в представление элемента управления дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Необходимые шаблоны элементов управления модели автоматизации пользовательского интерфейса  
 В следующей таблице перечислены шаблоны элементов управления [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], которые должны поддерживаться всеми элементами управления "Заголовок". Дополнительные сведения о шаблонах элементов управления см. в разделе [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Шаблон элемента управления|Поддержка|Примечания|  
|--------------------------------|---------------|----------------|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|Зависит от обстоятельств|Реализуйте этот шаблон элемента управления, если можно изменять размер элемента управления "Заголовок".|  
  
<a name="Required_UI_Automation_Events"></a>   
## Необходимые события модели автоматизации пользовательского интерфейса  
 В следующей таблице перечислены события [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], которые должны поддерживаться всеми элементами управления "Заголовок". Дополнительные сведения о событиях см. в разделе [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Событие [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Поддержка|Примечания|  
|-----------------------------------------------------------------------------------|---------------|----------------|  
|Событие изменения свойства <xref:System.Windows.Automation.AutomationElement.BoundingRectangleProperty>|Обязательно|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty>|Обязательно|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>|Обязательно|Нет|  
|<xref:System.Windows.Automation.AutomationElement.AutomationFocusChangedEvent>|Обязательный|Нет|  
|<xref:System.Windows.Automation.AutomationElement.StructureChangedEvent>|Обязательный|Нет|  
  
## См. также  
 <xref:System.Windows.Automation.ControlType.Header>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)