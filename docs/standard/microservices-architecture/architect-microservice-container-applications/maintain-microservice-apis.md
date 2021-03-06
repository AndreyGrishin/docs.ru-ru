---
title: "Создание развивается и управление версиями микрослужбу API-интерфейсы и контракты"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | Создание развивается и управление версиями микрослужбу API-интерфейсы и контракты"
keywords: "Docker, микрослужбы, ASP.NET, контейнер"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: 433711c3479eafd52bf9f5d53faf8e5707c6c624
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2017
---
# <a name="creating-evolving-and-versioning-microservice-apis-and-contracts"></a>Создание развивается и управление версиями микрослужбу API-интерфейсы и контракты

Микрослужбу API-Интерфейс представляет собой контракт между службой и своих клиентов. Можно развивать микрослужбу независимо друг от друга только в том случае, если не приводит к нарушению его API-Интерфейс контракта, почему так важно контракта. Если изменить контракт, повлияет клиентские приложения или шлюз API.

Характер определение API зависит от того, какой протокол используется. Например при использовании обмена сообщениями (например [AMQP](https://www.amqp.org/)), API состоит из типов сообщений. При использовании HTTP и службы RESTful API состоит из URL-адреса и форматах JSON запросов и ответов.

Тем не менее даже если вы собираетесь осторожно первоначальной контракта, API-Интерфейс службы будет необходимо изменить со временем. Когда это происходит, и особенно в том случае, если ваш API — это открытый API, используемые несколькими клиентскими приложениями, обычно не может заставить все клиенты должны обновить ваш новый контракт API. Обычно требуется последовательное развертывание новых версий службы, в результате которого старых и новых версиях контракта службы работают одновременно. Таким образом важно иметь стратегию для вашей службы управления версиями.

После изменения API имеют небольшой размер, например при добавлении атрибутов или параметры к вашему API, клиенты, использующие старую API должен перейдите и работать с новой версией службы. Можно предоставить значения по умолчанию для отсутствующих атрибутов, которые требуются, и клиенты смогут игнорировать любые атрибуты лишние ответа.

Однако иногда необходимо внести изменения на основной и несовместимый API-интерфейса службы. Поскольку вы не сможете принудительно клиентские приложения и службы, сразу же выполнить обновление до новой версии, службы должен поддерживать старые версии API-интерфейса для некоторого периода. Если используется механизм на основе HTTP, таких как REST, одним из подходов является внедрение номер версии API в URL-адрес или в заголовок HTTP. Затем можно выбрать между реализацией обе версии службы одновременно в один и тот же экземпляр службы или развертывание разных экземпляров, что каждый обрабатывать версии API-интерфейса. Для этого рекомендуется [шаблон посредником](https://en.wikipedia.org/wiki/Mediator_pattern) (например, [MediatR библиотеки](https://github.com/jbogard/MediatR)) для отделения версии другую реализацию в независимых обработчики.

Наконец, при использовании архитектуры REST [гипермедиа](https://www.infoq.com/articles/mark-baker-hypermedia) является оптимальным решением для управления версиями служб и позволяя развиваемой API-интерфейсы.

## <a name="additional-resources"></a>Дополнительные ресурсы

-   **Скотт Хансельман. Управление версиями основных RESTful веб-API ASP.NET, стало проще**
    <http://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx>

-   **Управление версиями API RESTful web**
    [*https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api*](https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api)

-   **Roy Fielding. Управление версиями, гипермедиа и REST**
    <https://www.infoq.com/articles/roy-fielding-on-versioning>


>[!div class="step-by-step"]
[Предыдущие] (асинхронной сообщения — на основе communication.md) [Далее] (микрослужбами адресация service-registry.md)
