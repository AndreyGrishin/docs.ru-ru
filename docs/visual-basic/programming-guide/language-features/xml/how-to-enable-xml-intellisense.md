---
title: "Практическое руководство. Включение XML IntelliSense в Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "IntelliSense [Visual Basic], XML"
  - "XML [Visual Basic], IntelliSense"
  - "XML IntelliSense [Visual Basic]"
ms.assetid: af67d0ee-a4a6-4abf-9c07-5a8cfe80d111
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# Практическое руководство. Включение XML IntelliSense в Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

XML\-технология IntelliSense в Visual Basic предоставляет возможность завершения слов для элементов, определенных в схеме XML.  Чтобы включить XML\-технологию IntelliSense в Visual Basic, выполните следующие действия.  
  
1.  Получите файл схемы XML \(XSD\) или файлы для файлов XML, которые приложение будет считывать или записывать.  
  
2.  Включите файлы схемы XML в проект.  
  
3.  Импортируйте конечное пространство имен или пространства имен в файл с текстом программы или в проект.  Конечное пространство имен определяется атрибутом `targetNamespace` или `tns` XSD\-схемы.  
  
     Чтобы импортировать конечное пространство имен, используйте оператор `Imports` или добавьте пространство имен для всех файлов кода в проекте при помощи страницы **Ссылки** в конструкторе проектов.  
  
 Дополнительные сведения о возможностях XML\-технологии IntelliSense в Visual Basic см. в разделе [XML IntelliSense в Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md).  Дополнительные сведения об импорте пространства имен XML см. в разделе [Оператор Imports \(пространство имен XML\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md) или [Страница "Ссылки" в конструкторе проектов \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic).  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
 ![ссылка на видео](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") Видеоверсию этой темы см. в разделе [Видеофайл практического руководства. Включение XML\-технологии IntelliSense в Visual Basic](http://go.microsoft.com/fwlink/?LinkId=102466) Связанную с этой темой видеодемонстрацию см. на веб\-странице [How Do I Enable XML IntelliSense and Use XML Namespaces?](http://go.microsoft.com/fwlink/?LinkId=143035).  
  
## Включение XML\-технологии IntelliSense в Visual Basic  
 Если имеется файл XML, но нет файла XSD\-схемы для него, в пакете обновлений 1 можно создать файл XSD\-схемы с помощью XML для мастера схемы.  Можно также использовать получение схемы в редакторе XML Visual Studio.  
  
#### Чтобы создать XSD\-схему для файла XML с помощью XML для мастера схем \(требуется пакет обновлений 1\)  
  
1.  В проекте в меню **Проект** выберите пункт **Добавить новый элемент**.  
  
2.  Выберите шаблон элемента **Xml to Schema** из категорий шаблонов **Данные** или **Общие элементы**.  
  
3.  Предоставьте имя файла для XSD\-файла или файлов, под которыми будет сохранена созданная схема и затем нажмите **Добавить**.  
  
4.  В окно **Определение набора XML\-схем из XML\-документов** добавьте один или больше XML\-документов, чтобы определить набор XML\-схем.  
  
    -   Добавлять текстовые файлы, содержащие XML\-документа с помощью обозревателя файла, нажмите кнопку **Добавить из файла**.  
  
    -   Чтобы добавить XML\-документ из http\-адреса, нажмите **Добавить из интернета**.  
  
    -   Чтобы скопировать или напечатать содержимое XML\-документа в мастере, нажмите **Ввод или вставка XML**.  
  
5.  После указания всех источников XML\-документов из которых нужно получить набор XML\-схем, нажмите кнопку **ОК**, чтобы получить набор XML\-схем.  Набор схем записывается в папке проекта в одном или нескольких XSD\-файлах.  \(для каждого пространства имен XML в заданной схеме создается XSD\-файл\).  
  
#### Чтобы создать XSD\-схему для файла XML с помощью получения схемы в редакторе XML Visual Studio  
  
1.  Измените файл XML в конструкторе XML в Visual Studio.  
  
2.  Когда курсор находится где\-нибудь в файле XML, появляется меню **XML**.  Нажмите кнопку **Создать схему** в меню **XML**.  XSD\-файл создается из XSD\-схемы из файла XML.  
  
3.  Сохраните файл XSD\-схемы.  
  
    > [!NOTE]
    >  Разные XSD\-схемы могут быть получены из нескольких документов XML, для которых используется одна и та же схема.  Это может произойти, если определенные элементы и атрибуты находятся в одном файле XML, а не в другом, или элементы включены в другом порядке.  При получении XSD\-схемы ее следует просмотреть на предмет полноты и точности.  
  
#### Чтобы включить файл XSD\-схемы  
  
-   По умолчанию XSD\-файлы в проектах Visual Basic не отображаются.  Если XSD\-файл уже имеется в папках для проекта, нажмите кнопку **Показать все файлы** в **обозревателе решений**.  Найдите XSD\-файл в **обозревателе решений**, щелкните правой кнопкой мыши файл и нажмите кнопку **Включить файл в проект**.  
  
-   Если XSD\-файл еще не является частью проекта, в **обозревателе решений** щелкните правой кнопкой мыши папку, в которой требуется сохранить XSD\-файл, выберите команду **Добавить**, а затем пункт **Существующий элемент**.  Найдите XSD\-файл и нажмите кнопку **Добавить**.  
  
#### Чтобы импортировать пространство имен XML в файле текста кода  
  
1.  Укажите конечное пространство имен из XSD\-схемы.  
  
2.  В начале файла кода добавьте оператор `Imports` для конечного пространства имен XML, как показано в следующем примере.  
  
     [!code-vb[VbXMLSamples#1](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-enable-xml-intell_1.vb)]  
  
     Чтобы импортировать пространство имен XML как пространство имен по умолчанию \(т.е. пространство имен, которое применяется к элементам XML и атрибутам, у которых нет префикса пространства имен\), добавьте оператор `Imports` для конечного пространства имен XML по умолчанию.  Не указывайте префикс пространства имен.  Ниже приведен пример оператора `Imports`.  
  
     [!code-vb[VbXmlSamples#50](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/how-to-enable-xml-intell_2.vb)]  
  
#### Чтобы импортировать пространство имен XML для всех файлов в проекте  
  
1.  Пространство имен XML, импортированное в файл кода, относится к только к этому файлу кода.  Чтобы импортировать пространство имен XML для всех файлов кода в проекте, дважды щелкните **Мой проект** в **обозревателе решений**, чтобы открыть конструктор проектов.  
  
2.  На вкладке **Ссылки**, в поле **Импортированные пространства имен** введите конечное пространство имен XML в виде полного объявления пространства имен XML \(например, `<xmlns: ns="http://sampleNamespace">`\).  Если конечное пространство имен XML не указывает префикс пространства имен, то оно будет использоваться как пространство имен XML по умолчанию для проекта.  
  
3.  Нажмите кнопку **Добавить пользовательский импорт**.  
  
## См. также  
 [Оператор Imports \(пространство имен XML\)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Страница "Ссылки" в конструкторе проектов \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)   
 [XML IntelliSense в Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)