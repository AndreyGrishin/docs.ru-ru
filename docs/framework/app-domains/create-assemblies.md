---
title: "Создание сборок"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- single-file assemblies
- assemblies [.NET Framework], creating
- multifile assemblies
ms.assetid: 54832ee9-dca8-4c8b-913c-c0b9d265e9a4
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2168cbcd19437c1e275da7a01aa0c75ab47600eb
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="creating-assemblies"></a>Создание сборок
Можно создать однофайловую или многофайловую сборку с помощью интегрированной среды разработки IDE, такой как [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)], или с помощью компиляторов и средств, предоставляемых [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]. Простейшая сборка представляет собой один файл, имеющий простое имя и загружаемый в единственный домен приложения. На эту сборку нельзя ссылаться из других сборок, находящихся вне папки приложения; кроме того, к ней неприменим механизм проверки версий. Для удаления приложения, состоящего из сборки, достаточно просто удалить папку, в которой оно располагается. Для большинства разработчиков сборки с такими возможностями достаточно для развертывания приложения.  
  
 Многофайловую сборку можно создать на основе нескольких модулей кода и файлов ресурсов. Кроме того, можно создать сборку, которая будет совместно использоваться несколькими приложениями. Совместно используемая сборка должна иметь строгое имя и должна быть развернута в глобальном кэше сборок.  
  
 Существует несколько способов объединения модулей кода и ресурсов в сборки; способ зависит от следующих факторов.  
  
-   Управление версиями  
  
     Объединение модулей, имеющих одни и те же сведения о версии.  
  
-   Развертывание  
  
     Объединение модулей кода и ресурсов, поддерживающих данную модель развертывания.  
  
-   Повторное использование  
  
     Объединение модулей, если они могут логически использоваться совместно для некоторых целей. Например, сборка, состоящая из типов и классов, редко используемых для сопровождения программы, может быть помещена в ту же самую сборку. Кроме того, типы, предназначенные для совместного использования несколькими приложениями, могут быть объединены в сборку, которая должна быть подписана строгим именем.  
  
-   Безопасность  
  
     Объединение модулей, содержащих типы, которым требуются одни и те же разрешения безопасности.  
  
-   Область действия  
  
     Объединение модулей, содержащих типы, область видимости которых должна быть ограничена этой же сборкой.  
  
 Необходимо обратить особое внимание при предоставлении доступа к сборкам среды CLR из неуправляемых COM-приложений. Дополнительные сведения о работе с неуправляемым кодом содержатся в разделе [Предоставление COM-клиентам доступа к компонентам .NET Framework](../../../docs/framework/interop/exposing-dotnet-components-to-com.md).  
  
## <a name="see-also"></a>См. также  
 [Программирование с использованием сборок](../../../docs/framework/app-domains/programming-with-assemblies.md)  
 [Управление версиями сборок](../../../docs/framework/app-domains/assembly-versioning.md)  
 [Практическое руководство. Построение однофайловой сборки](../../../docs/framework/app-domains/how-to-build-a-single-file-assembly.md)  
 [Практическое руководство. Создание многофайловой сборки](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)  
 [Обнаружение сборок в среде выполнения](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
 [Многофайловые сборки](../../../docs/framework/app-domains/multifile-assemblies.md)
