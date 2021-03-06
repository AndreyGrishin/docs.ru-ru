---
title: "Оптимизация производительности: привязка данных"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding data [WPF], performance
- data binding [WPF], performance
ms.assetid: 1506a35d-c009-43db-9f1e-4e230ad5be73
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: c420748a9361655eeb2df33ce8426d9f167d3414
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="optimizing-performance-data-binding"></a>Оптимизация производительности: привязка данных
Привязка данных [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] предоставляет приложениям простой и последовательный способ представления данных и взаимодействия с ними. Можно связывать элементы с данными из различных источников данных в виде объектов [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] и [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)].  
  
 В этом разделе даются рекомендации по повышению производительности привязки данных.  
  

  
<a name="HowDataBindingReferencesAreResolved"></a>   
## <a name="how-data-binding-references-are-resolved"></a>Как разрешаются ссылки для привязки данных  
 Прежде чем обсуждать вопросы производительности привязки данных, стоит изучить, как механизм привязки данных [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] разрешает ссылки на объекты для привязки.  
  
 Источником привязки данных [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] может быть любой объект [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]. Можно выполнять привязку к свойствам, вложенным свойствам или индексаторам объекта [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]. Ссылки привязки разрешаются с помощью [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)] отражения или <xref:System.ComponentModel.ICustomTypeDescriptor>. Ниже приведены три метода для разрешения ссылок на объекты для привязки.  
  
 Первый метод включает использование отражения. В этом случае <xref:System.Reflection.PropertyInfo> объект используется для обнаружения атрибуты свойства и обеспечивает доступ к метаданным свойства. При использовании <xref:System.ComponentModel.ICustomTypeDescriptor> интерфейс, механизм привязки данных использует этот интерфейс для доступа к значениям свойств. <xref:System.ComponentModel.ICustomTypeDescriptor> Интерфейс особенно полезна в случаях, когда объект не имеют постоянного набора свойств.  
  
 Уведомления об изменении свойств могут быть предоставлены с реализацией <xref:System.ComponentModel.INotifyPropertyChanged> интерфейс или с помощью уведомления об изменениях, связанных с <xref:System.ComponentModel.TypeDescriptor>. Однако предпочтительная стратегия для реализации уведомления об изменении свойств является использование <xref:System.ComponentModel.INotifyPropertyChanged>.  
  
 Если исходный объект не [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] объект и свойство source — [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] свойство, [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] механизм привязки данных должен сначала использовать отражение для исходного объекта, чтобы получить <xref:System.ComponentModel.TypeDescriptor>, а затем запросить <xref:System.ComponentModel.PropertyDescriptor>. Эта последовательность операций отражения может занимать очень много времени с точки зрения производительности.  
  
 Второй метод для разрешения ссылок на объекты включает в себя [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] исходного объекта, который реализует <xref:System.ComponentModel.INotifyPropertyChanged> интерфейс и исходное свойство, которое является [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] свойства. В этом случае механизм привязки данных использует отражение непосредственно в исходном типе и возвращает необходимое свойство. Это по-прежнему не самый оптимальный метод, но он предъявляет меньше требований к рабочему набору, чем первый метод.  
  
 Третий метод для разрешения ссылок на объекты включает исходный объект, <xref:System.Windows.DependencyObject> и исходное свойство, которое является <xref:System.Windows.DependencyProperty>. В этом случае механизму привязки данных не нужно использовать отражение. Вместо этого механизм свойства и механизм привязки данных оба разрешают ссылку на свойство независимо. Это оптимальный метод для разрешения ссылок на объекты, используемые для привязки данных.  
  
 В следующей таблице сравнивается скорость привязки данных <xref:System.Windows.Controls.TextBlock.Text%2A> свойство тысяч <xref:System.Windows.Controls.TextBlock> элементов с помощью следующих трех методов.  
  
|**Привязка свойства Text объекта TextBlock**|**Время привязки (мс)**|**Время отрисовки — включает привязку (мс)**|  
|--------------------------------------------------|-----------------------------|--------------------------------------------------|  
|К свойству объекта [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]|115|314|  
|К свойству [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] объекта, который реализует<xref:System.ComponentModel.INotifyPropertyChanged>|115|305|  
|Чтобы <xref:System.Windows.DependencyProperty> из <xref:System.Windows.DependencyObject>.|90|263|  
  
<a name="Binding_to_Large_CLR_Objects"></a>   
## <a name="binding-to-large-clr-objects"></a>Привязка к большим объектам среды CLR  
 Привязка данных к одному объекту [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] с тысячами свойств значительно влияет на производительность. Это влияние можно минимизировать путем разделения одного объекта на несколько объектов [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] с меньшим количеством свойств. В таблице показаны время привязки и время отрисовки для привязки данных к одному большому объекту [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] и к нескольким небольшим объектам.  
  
|**Привязка данных 1000 объектов TextBlock**|**Время привязки (мс)**|**Время отрисовки — включает привязку (мс)**|  
|---------------------------------------------|-----------------------------|--------------------------------------------------|  
|К объекту [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] с 1000 свойств|950|1200|  
|К 1000 объектов [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] с одним свойством|115|314|  
  
<a name="Binding_to_an_ItemsSource"></a>   
## <a name="binding-to-an-itemssource"></a>Привязка к ItemsSource  
 Рассмотрим сценарий, в котором имеется [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> объект, содержащий список сотрудников, которые должны отображаться в <xref:System.Windows.Controls.ListBox>. Чтобы установить соответствие между этими двумя объектами, можно привязать список сотрудников к <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> свойство <xref:System.Windows.Controls.ListBox>. Предположим, что к группе присоединяется новый сотрудник. Может показаться, что чтобы вставить этого человека в список связанных <xref:System.Windows.Controls.ListBox> значения, необходимо просто добавить этого пользователя в список сотрудников и ожидать, что это изменение автоматически распознается ядром привязки данных. Это предположение оказалось бы false; в действительности, изменения не отражаются в <xref:System.Windows.Controls.ListBox> автоматически. Это вызвано [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> объект автоматически не вызывает события изменения коллекции. Для получения <xref:System.Windows.Controls.ListBox> для регистрации изменений, получится повторно создать список сотрудников и присоединить его к <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> свойство <xref:System.Windows.Controls.ListBox>. Хотя это решение работает, оно серьезно влияет на производительность. Каждый раз при присваивании <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> из <xref:System.Windows.Controls.ListBox> новый объект, <xref:System.Windows.Controls.ListBox> сначала отбрасывает предыдущие элементы и повторно создает весь список. Влияние на производительность увеличивается, если ваш <xref:System.Windows.Controls.ListBox> сопоставляется со сложным <xref:System.Windows.DataTemplate>.  
  
 Эффективным решением этой проблемы является преобразование списка сотрудников <xref:System.Collections.ObjectModel.ObservableCollection%601>. <xref:System.Collections.ObjectModel.ObservableCollection%601> Объект создает уведомление об изменениях, который можно получать механизм привязки данных. Событие добавляет или удаляет элемент из <xref:System.Windows.Controls.ItemsControl> без необходимости восстановления всего списка.  
  
 В таблице ниже показано время, необходимое для обновления <xref:System.Windows.Controls.ListBox> (с отключенной виртуализацией пользовательского интерфейса) при добавлении элемента. Число в первой строке представляет время, прошедшее после [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> объект привязан к <xref:System.Windows.Controls.ListBox> элемента <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>. Число во второй строке представляет время, прошедшее после <xref:System.Collections.ObjectModel.ObservableCollection%601> привязан к <xref:System.Windows.Controls.ListBox> элемента <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>. Заметки сэкономить значительное время с помощью <xref:System.Collections.ObjectModel.ObservableCollection%601> стратегии привязки данных.  
  
|**Привязка данных ItemsSource**|**Время обновления для 1 элемента (мс)**|  
|--------------------------------------|---------------------------------------|  
|Чтобы [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] <xref:System.Collections.Generic.List%601> объекта|1656|  
|Для<xref:System.Collections.ObjectModel.ObservableCollection%601>|20|  
  
<a name="Binding_IList_to_ItemsControl_not_IEnumerable"></a>   
## <a name="bind-ilist-to-itemscontrol-not-ienumerable"></a>Привязка IList к ItemsControl не IEnumerable  
 Если у вас есть выбор между привязкой <xref:System.Collections.Generic.IList%601> или <xref:System.Collections.IEnumerable> для <xref:System.Windows.Controls.ItemsControl> , следует выбрать <xref:System.Collections.Generic.IList%601> объекта. Привязка <xref:System.Collections.IEnumerable> для <xref:System.Windows.Controls.ItemsControl> принудительно [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] для создания оболочки <xref:System.Collections.Generic.IList%601> объекта, то есть производительность подвержено влиянию ненужных затрат ресурсов для второго объекта.  
  
<a name="Do_not_Convert_CLR_objects_to_Xml_Just_For_Data_Binding"></a>   
## <a name="do-not-convert-clr-objects-to-xml-just-for-data-binding"></a>Не преобразовывайте объекты среды CLR в XML только для привязки данных.  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] позволяет привязать данные к содержимому [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]; однако привязка данных к содержимому [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] выполняется медленнее, чем привязка данных к объектам [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]. Не преобразуйте данные объекта [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] в XML, если единственной целью этого является привязка данных.  
  
## <a name="see-also"></a>См. также  
 [Улучшение производительности приложений WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)  
 [Планирование производительности приложения](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)  
 [Использование преимуществ оборудования](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)  
 [Разметка и разработка](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)  
 [Двумерная графика и изображения](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)  
 [Поведение объекта](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)  
 [Ресурсы приложений](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)  
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)  
 [Дополнительные рекомендации по повышению производительности](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)  
 [Общие сведения о привязке данных](../../../../docs/framework/wpf/data/data-binding-overview.md)  
 [Пошаговое руководство. Кэширование данных приложения WPF](../../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)
