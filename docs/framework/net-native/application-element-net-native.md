---
title: "Элемент &lt;Application&gt; (машинный код .NET) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b4e9b37a-059b-4076-8f56-cb3f9cef0cd9
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Элемент &lt;Application&gt; (машинный код .NET)
Служит в качестве контейнера для типов и членов типов приложения, метаданные которого доступны для отражения во время выполнения и применяет политику отражения среды выполнения ко всем программным элементам приложения.  
  
 <>\>Элемент  
<>\>Элемент (rd.xml)  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Application Activate="policy_setting"  
             Browse="policy_setting"  
             Dynamic="policy_setting"  
             Serialize="policy_setting"  
             DataContractSerializer="policy_setting"  
             DataContractJsonSerializer="policy_setting"  
             XmlSerializer="policy_setting"  
             MarshalObject="policy_setting"  
             MarshalDelegate="policy_setting"  
             MarshalStructure="policy_setting" />  
  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы. В таблице дочерних элементов политика имеет отношение к метаданным, к которым программные элементы получают доступ по время выполнения.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Тип атрибута|Описание|  
|---------------|--------------------|-----------------|  
|`Activate`|Отражение|Необязательный атрибут. Управляет доступом среды выполнения к конструкторам для включения активации экземпляров.|  
|`Browse`|Отражение|Необязательный атрибут. Определяет запрос для получения сведений о типах или перечисляет типы, но не включает динамический доступ во время выполнения.|  
|`Dynamic`|Отражение|Необязательный атрибут. Управляет доступом среды выполнения ко всем членам типа, включая конструкторы, методы, поля, свойства и события, чтобы включить динамическое программирование.|  
|`Serialize`|Сериализация|Необязательный атрибут. Управляет доступом среды выполнения к конструкторам, полям и свойствам, позволяющим сериализовать и десериализовать экземпляры типа с помощью таких библиотек, как, например, сериализатор Newtonsoft JSON.|  
|`DataContractSerializer`|Сериализация|Необязательный атрибут Определяет политику для сериализации, который использует <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> класса.|  
|`DataContractJsonSerializer`|Сериализация|Необязательный атрибут Определяет политику для сериализации JSON, который использует <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> класса.|  
|`XmlSerializer`|Сериализация|Необязательный атрибут Определяет политику для сериализации XML, который использует <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> класса.|  
|`MarshalObject`|Interop|Необязательный атрибут Определяет политику для маршалинга ссылочных типов в среды выполнения Windows и COM.|  
|`MarshalDelegate`|Interop|Необязательный атрибут Определяет политики для маршалинга типов делегатов как указателей функции на машинный код.|  
|`MarshalStructure`|Interop|Необязательный атрибут Определяет политику для маршалинга структуры в машинный код.|  
  
## <a name="all-attributes"></a>Все атрибуты  
  
|Значение|Описание|  
|-----------|-----------------|  
|*policy_setting*|Параметр для этой политики, относящихся к типам в приложении. Допустимые значения `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` и `Required All`. Дополнительные сведения см. в разделе [параметры политики директив среды выполнения](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/assembly-element-net-native.md)|Применяет политику ко всем типам в определенной сборке.|  
|[<>\>](../../../docs/framework/net-native/namespace-element-net-native.md)|Применяет политику ко всем типам в определенном пространстве имен.|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Применяет политику для конкретного типа, например, класса или структуры.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Применяет политику к сконструированному универсальному типу. Например [ <> \> ](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) элемент может использоваться для задания политики для `List<String>` типа.|  
|[<>\>](../../../docs/framework/net-native/method-element-net-native.md)|Применяет политику к методу определенного типа.|  
|[<>\>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)|Применяет политику к сконструированному универсальному методу.|  
|[<>\>](../../../docs/framework/net-native/property-element-net-native.md)|Применяет политику к свойству определенного типа.|  
|[<>\>](../../../docs/framework/net-native/field-element-net-native.md)|Применяет политику к полю определенного типа.|  
|[<>\>](../../../docs/framework/net-native/event-element-net-native.md)|Применяет политику к событию определенного типа.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/directives-element-net-native.md)|Корневой элемент файла директив среды выполнения.|  
  
## <a name="remarks"></a>Примечания  
 [ <> \> ](../../../docs/framework/net-native/directives-element-net-native.md) Элемент может содержать ноль или один `<Application>` элемента. Несколько элементов `<Application>` в одном файле директив отражения не поддерживаются.  
  
 Элемент `<Application>` можно использовать одним из двух способов:  
  
-   В качестве контейнера для определения программных элементов, метаданные которых требуются во время выполнения. В этом случае элементу `<Application>` необязательно иметь какие-либо атрибуты. Во время компиляции средства компилятора выполняют поиск всех библиотек, в том числе основных библиотек .NET Framework, на наличие программных элементов, определенных дочерними элементами элемента `<Application>`. Напротив, средства компилятора выполняют поиск только тех библиотек, обозначенный [ <> \> ](../../../docs/framework/net-native/library-element-net-native.md) наличие программных элементов, определенных дочерними элементами элемента [ <> \</> \> ](../../../docs/framework/net-native/library-element-net-native.md).  
  
-   Как элемент, который задает политику уровня приложения для отражения, сериализации и взаимодействия. Атрибуты `<Application>` элемент определяют политику уровня приложения, которая может быть переопределена дочерние элементы, определенные в `<Application>` или [ <> \> ](../../../docs/framework/net-native/library-element-net-native.md) элемента.  
  
## <a name="see-also"></a>См. также  
 [<>\>Элемент](../../../docs/framework/net-native/library-element-net-native.md)   
 [<>\>Элемент](../../../docs/framework/net-native/directives-element-net-native.md)   
 [Элементы директив среды выполнения](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Ссылка на файл конфигурации директив (rd.xml) среды выполнения](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)