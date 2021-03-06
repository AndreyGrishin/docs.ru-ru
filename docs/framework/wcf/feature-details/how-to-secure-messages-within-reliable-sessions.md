---
title: "Практическое руководство. Защита сообщений с помощью надежных сеансов"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aee33e50-936f-4486-9ca8-c1520c19a62d
caps.latest.revision: "8"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 2604b9dacf11b9971b10d23d9a807092ddf07830
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-secure-messages-within-reliable-sessions"></a>Практическое руководство. Защита сообщений с помощью надежных сеансов

В этом разделе описывается обеспечение безопасности на уровне сообщения в ходе надежного сеанса обмена сообщениями с использованием одной из предоставляемых системой привязок, которые поддерживают такие сеансы, но не по умолчанию. Включите защищенный, надежный сеанс можно принудительно с помощью кода или декларативно в файле конфигурации. В этой процедуре для разрешения защищенного, надежного сеанса используются файлы конфигурации клиента и службы.

Эта процедура включает выполнение трех основных задач, а именно:

1. необходимо задать, что клиент и служба обмениваются сообщениями в ходе надежного сеанса;

1. необходимо обеспечить безопасность на уровне сообщения в ходе надежного сеанса;

1. необходимо задать тип учетных данных клиента, который должен использоваться при проверке подлинности клиента в службе.

Очень важно в первой задаче, которая содержит элемент конфигурации конечной точки `bindingConfiguration` атрибут, ссылающийся на конфигурацию привязки с именем (в данном примере) `MessageSecurity`. [  **\<Привязки >** ](../../../../docs/framework/misc/binding.md) элемента конфигурации, затем ссылается на это имя, чтобы разрешить надежные сеансы, задав `enabled` атрибут [  **\<reliableSession >** ](http://msdn.microsoft.com/library/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b) элемент `true`. Можно потребовать гарантии упорядоченной доставки сообщений в ходе надежного сеанса, присвоив атрибуту `ordered` значение `true`.

Исходная копия примера, лежащие в основе этой процедуры настройки в разделе [надежный сеанс WS](../../../../docs/framework/wcf/samples/ws-reliable-session.md).

Основные элементы вторая задача выполняется, задав `mode` атрибут  **\<безопасности >** элемента, содержащегося в  **\<привязки >** элемент клиента и службы для `Message`.

Основные элементы третья задача выполняется, задав `clientCredentialType` атрибут  **\<сообщения >** элемента, содержащегося в  **\<безопасности >** элемент клиента и службы для `Certificate`.

> [!NOTE]
> При использовании безопасности сообщений с надежных сеансов, надежный обмен сообщениями пытается проверить подлинность несанкционированный клиент до истечения периода ожидания, а не вызывает исключение после первой неудачной попытки.

### <a name="configure-the-service-with-a-wshttpbinding-to-use-a-reliable-session"></a>Настройка службы с привязкой WSHttpBinding использования надежного сеанса

Эта процедура описана в [как: обмена сообщениями в рамках надежного сеанса](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md).

### <a name="configure-the-client-with-a-wshttpbinding-to-use-a-reliable-session"></a>Настройка клиента с привязкой WSHttpBinding использования надежного сеанса

Эта процедура описана в [как: обмена сообщениями в рамках надежного сеанса](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md).

### <a name="set-the-mode-and-clientcredentialtype-in-configuration"></a>Установка режима и свойства ClientCredentialType в конфигурации

1. Добавить элемент привязки [  **\<привязки >** ](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) элемента файла конфигурации. В следующем примере добавляется [  **\<wsHttpBinding >** ](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) элемента.

1. Добавить  **\<привязки >** и присвойте его `name` соответствующее значение атрибута. В примере используется имя `MessageSecurity`.

1. Добавить  **\<безопасности >** и присвойте `mode` атрибут `Message`.

1. В пределах  **\<безопасности >** элемента, добавьте  **\<сообщения >** и присвойте `clientCredentialType` атрибут `Certificate`.

```xml
<wsHttpBinding>
  <binding name="MessageSecurity">
    <security mode="Message">
      <message clientCredentialType="Certificate" />
    </security>
  </binding>
</wsHttpBinding>
```
