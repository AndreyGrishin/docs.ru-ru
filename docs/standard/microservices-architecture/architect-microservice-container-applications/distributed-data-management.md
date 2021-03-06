---
title: "Проблемы и решения для управления распределенными данными"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | Проблемы и решения для управления распределенными данными"
keywords: "Docker, микрослужбы, ASP.NET, контейнер"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: f961475b40c74bf448cff1aeae04ae4866360e52
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2017
---
# <a name="challenges-and-solutions-for-distributed-data-management"></a>Проблемы и решения для управления распределенными данными

## <a name="challenge-1-how-to-define-the-boundaries-of-each-microservice"></a>Запрос \#1: способ определения границ каждого микрослужбу

Определение границ микрослужбу является первой проверки, возникающих в любой пользователь. Каждый микрослужбу должно быть части приложения и каждого микрослужбу должен быть автономной все преимущества и проблемы, которые он предоставляет. Но как определить эти границы?

Во-первых необходимо сосредоточиться на моделях логического домена приложения и связанные данные. Необходимо попытаться выявить несвязанной острова данных и различных контекстах внутри одного приложения. В каждом контексте могут иметь различные языка (различные бизнес-терминологией). Контексты должен быть определяются и управляются независимо друг от друга. Термины и объекты, используемые в этих контекстах может показаться аналогичный, но может оказаться, что в указанном контексте бизнес-концепция, с одним используется для другой цели в другом контексте и даже может иметь другое имя. Например пользователя можно обращаться как пользователь в контексте удостоверения или членства как клиента в контексте CRM, в качестве покупателей в контексте порядка сортировки и так далее.

Способ определения границ между несколькими контекстами приложение с другим доменом, для каждого контекста именно идентифицируете границы для каждого микрослужбу бизнеса и связанные с ним модели домена и данных. Всегда пытаются минимизировать связь между этими микрослужбами. В этом руководстве приведены более подробные сведения об этом проектирования модели идентификации и домена в разделе [определение границ модель домена для каждого микрослужбу](#identifying-domain-model-boundaries-for-each-microservice) позже.

## <a name="challenge-2-how-to-create-queries-that-retrieve-data-from-several-microservices"></a>Запрос \#2: создание запросов, получающих данные из нескольких микрослужбами

Второй запрос — способы реализации запросов, получающих данные из нескольких микрослужбами избегая частый обмен данными микрослужбами от удаленного клиентского приложения. Пример может быть на одном экране из мобильного приложения, который необходимо показать сведения о пользователе, владельцем которого является корзины, каталогом и микрослужбами удостоверение пользователя. Другим примером может служить сложных отчетов, связанных с большим количеством таблиц, расположенных в нескольких микрослужбами. Решение зависит от сложности запросов. Однако в любом случае потребуется способ статистические данные, если вы хотите повысить эффективность обмена данными вашей системы. Ниже перечислены наиболее популярных решений.

**Шлюз API**. Для статистической обработки данных из нескольких микрослужбами, принадлежат разным базам данных рекомендуется микрослужбу статистической обработки, называются шлюз API. Тем не менее необходимо уделять особое внимание реализации этот шаблон, так как он может быть моментом стягиванием системы и он может нарушать принцип микрослужбу автономность. Чтобы устранить такую возможность, может иметь несколько шлюзов API Контролируемая влечет каждого один сосредоточиться на «срез» по вертикали или области деятельности системы. Шаблон шлюза API является более подробно в разделе Using шлюз API в более поздней версии.

**CQRS с таблицами, запрос чтения**. Еще одно решение для статистической обработки данных из нескольких микрослужбами — [материализованные представления шаблон](https://docs.microsoft.com/azure/architecture/patterns/materialized-view). При таком подходе можно создать, заранее (Подготовка денормализованные данные до возникновения фактическими запросами), с данными, владельцем которого является несколько микрослужбами таблицы только для чтения. Таблица имеет формат, соответствующий потребностям в клиентском приложении.

Рассмотрим нечто похожее на экране для мобильного приложения. При наличии одной базы данных может объединяют данные для данного экрана, с помощью SQL-запрос, выполняющий сложного соединения с использованием нескольких таблиц. Тем не менее если у вас есть несколько баз данных, а каждая база данных принадлежит другой микрослужбу, нельзя запрашивать эти базы данных и создавать соединения SQL. Сложный запрос становится проблемой. Можно решить требования, используя подход CQRS — создать денормализованные таблицу в другой базе данных, который используется только для запросов. Таблицы могут быть разработаны специально для данных, необходимые для сложных запросов, с отношением один к одному между полями, требуется экрана приложения и столбцы в таблице запрос. Его также можно использовать для создания отчетов.

Этот подход не только позволяет решить проблемы (как запроса и соединения между микрослужбами); также повышает производительность значительно при сравнении с сложного соединения, поскольку уже есть данные, приложение должно таблицы запроса. Конечно с помощью команды и разделение ответственности запросов (CQRS) с таблицами, запрос чтения означает дополнительная разработка, и вам потребуется принять окончательной согласованности. Тем не менее требования к производительности и высокого уровня масштабируемости в [совместной](http://udidahan.com/2011/10/02/why-you-should-be-using-cqrs-almost-everywhere/) (или конкуренция в зависимости от того, с точки зрения) — где следует применять CQRS с несколькими базами данных.

**«Холодный данных» в центре баз данных**. Сложные отчеты и запросы, которые могут не требовать данные в реальном времени, распространенным подходом является экспорт вашей «горячих данных» (данные о транзакциях из микрослужбами) как «холодных» данных в больших баз данных, которые используются только для отчетов. Система, центральная база данных может быть систему большие наборы данных, таких как Hadoop, хранилище данных как на основе хранилища данных SQL Azure или даже одной базы данных SQL используется только для отчетов (если размер не будет проблемой).

Имейте в виду, что эта централизованная база данных будет использоваться только для запросов и отчетов, не требующие данные в реальном времени. Исходные обновления и транзакции, как ваш источник достоверных, должны быть в микрослужбами данных. Способ, выполняется синхронизация данных будет с помощью связи с событиями (рассматривается в следующих разделах) или с помощью других средств импорта и экспорта инфраструктуры базы данных. Если используется связь с событиями, процесс этой интеграции будет выглядеть так же как при распространении данных, как описано выше для таблиц CQRS запроса.

Тем не менее, если при разработке приложения включает в себя постоянно агрегация сведений из нескольких микрослужбами для сложных запросов, может быть признаком плохого проекта — микрослужбу должно быть в качестве изолированных максимально из других микрослужбами. (При этом исключаются отчетов или анализа, всегда следует использовать центра данных холодного баз данных). Часто наличие этой проблемы может быть причина для объединения микрослужбами. Необходимо соблюдать баланс между автономность развитие и развертывание каждого микрослужбу строгой зависимости, связности и объединение данных.

## <a name="challenge-3-how-to-achieve-consistency-across-multiple-microservices"></a>Запрос \#3: как для поддержания согласованности между несколькими микрослужбами

Как уже говорилось ранее, данных, владельцем каждого микрослужбу является закрытым для этого микрослужбу и возможен только с помощью его микрослужбу API. Таким образом представленных сложной задачей является способ реализации конца в конец бизнес-процессов, сохраняя согласованность между несколькими микрослужбами.

Чтобы проанализировать эту проблему, давайте рассмотрим пример из [eShopOnContainers обращение к приложению](http://aka.ms/eshoponcontainers). Каталог микрослужбу сохраняет сведения о всех продуктах, включая их уровень запасов. Упорядочение микрослужбу управляет заказов и необходимо убедиться, что нового заказа не превышает акции продукции доступный каталог. (Или сценарий может включать логику, которая обрабатывает Задолженный продуктов). В гипотетической монолитные версии этого приложения подсистемы порядка сортировки может просто использовать транзакции ACID Проверьте доступность на складе, создания заказа в таблице Orders и обновить имеющиеся товары в таблице Products.

Однако в приложении микрослужбами на основе таблиц заказов и продуктов принадлежат их соответствующих микрослужбами. Никогда не микрослужбу следует баз данных, принадлежащих другой микрослужбу в транзакции или запросы, как показано на рисунке 4 – 9.

![](./media/image9.PNG)

**На рисунке 4 – 9**. Микрослужбу не может напрямую обращаться к таблице в другой микрослужбу

Микрослужбу упорядочения элементов не должны обновлять таблицы Products напрямую, так как в таблице продуктов принадлежит микрослужбу каталога. Чтобы внести обновления каталога микрослужбу, микрослужбу упорядочения элементов только когда-либо следует использовать асинхронное взаимодействие, таких как события интеграции (сообщение и связи на основе события). Это как [eShopOnContainers](http://aka.ms/eshoponcontainers) ссылка приложения выполняет этот тип обновления.

Как уже говорилось [Крепления Теорема](https://en.wikipedia.org/wiki/CAP_theorem), необходимо выбрать между доступностью и ACID строгая согласованность. Большинство сценариев, основанных на микрослужбу требуется доступности и высокую масштабируемость, в отличие от строгая согласованность. Критически важные приложения должны оставаться копии и запуска и разработчиков можно обойти строгая согласованность с помощью методов для работы со слабой или окончательной согласованности. Именно этот подход, выполняемое большинство архитектуры на основе микрослужбы.

Кроме того, стиль ACID или двухфазной фиксации транзакции не только с принципами микрослужбами; в большинстве баз данных NoSQL (например, базу данных Azure Cosmos, MongoDB, т. д.) не поддерживают двухфазной фиксации транзакции. Тем не менее обслуживание данных очень важно согласованность разных служб и баз данных. Этот запрос также связана с вопрос, как распространить изменения через несколько микрослужбами, если некоторые данные должны быть избыточным — например, при необходимости иметь имя или описание в каталоге микрослужбу и корзине продукта микрослужбы.

Хорошим решением этой проблемы является использование окончательной согласованности между микрослужбами определена через связи с событиями и системой публикации и подписки. В этих разделах рассматриваются в разделе [асинхронной связи с событиями](#async_event_driven_communication) далее в этом руководстве.

## <a name="challenge-4-how-to-design-communication-across-microservice-boundaries"></a>Запрос \#4: как создавать связи через границы микрослужбу

Границы, обмена данными через микрослужбу является серьезной проблемой. В этом контексте связи не ссылается на то, что вы протокола следует использовать (HTTP и REST, AMQP обмена сообщениями и т. д.). Вместо этого адреса, какой стиль связи, следует использовать, и особенно как связанная вашей микрослужбами должна быть. В зависимости от уровня соединения если происходит сбой, влияние, сбой в системе будет сильно различаться.

В распределенной системе как микрослужбами-приложении с настолько большое количество артефактов, перемещения и распределенные службы через несколько серверов или узлы компоненты со временем не удастся. Частичный сбой и еще больше простои возникает, так, следует создать ваш микрослужбами и связи между ними принимая во внимание риски общих такого распределенной системе.

Популярный подход заключается в реализации HTTP (REST)-микрослужбами из-за простоты их основе. Подход на основе HTTP, полностью приемлемо; Здесь проблема связана с ее использование. При использовании запросов и ответов HTTP только для взаимодействия с вашей микрослужбами из клиентских приложений, или из API шлюзов, это нормально. Однако при создании длинных цепочек синхронные вызовы HTTP через микрослужбами обмена данными через границами, как будто микрослужбами объектов в приложении монолитные приложения будет в конечном счете возникли проблемы.

Для экземпляра представьте, что клиентское приложение отправляет вызов HTTP API на отдельных микрослужбу как микрослужбу упорядочения элементов. Если микрослужбу упорядочения элементов в свою очередь вызывает дополнительных цикла микрослужбами через HTTP в пределах того же запрос ответ, вы создаете цепочки вызовов HTTP. Это может показаться разумным изначально. Однако есть важные моменты, которые следует учитывать при выхода из строя этот путь:

-   Блокировки и низкой производительности. Из-за особенностей синхронные HTTP первоначальный запрос не получит ответ, завершения внутренние вызовы HTTP. Предположим, если количество этих вызовов существенно повышает и в то же время, один из промежуточного HTTP вызовы микрослужбу блокируется. Результатом является влияет на производительность, что общая масштабируемость экспоненциально повлияют на дополнительных увеличение запросы HTTP.

-   Взаимозависимость микрослужбами с HTTP. Business микрослужбами не должен быть связан с другим микрослужбами бизнеса. В идеальном случае они должны «неизвестно» о существовании других микрослужбами. Если приложение использует взаимозависимость микрослужбами, как показано в примере, достижение автономность каждого микрослужбу будет практически невозможно.

-   Сбой при любой один микрослужбы. Если реализован цепочки микрослужбами, связанных с HTTP-обращениях при сбое любой микрослужбами (а в конечном итоге произойдет сбой) вся цепочка микрослужбами завершится ошибкой. Необходимо предусмотреть системой микрослужбу и продолжить работу, а также возможные во время частичных сбоев. Даже если реализовать логику клиент, использующий повторные попытки с экспоненциально растущим или механизмы Размыкатель цепи, дополнительные цепочки вызовов комплексного HTTP будет, тем сложнее его будет реализовать стратегию сбоя, основанный на HTTP.

На самом деле Если вашей внутренней микрослужбами обмениваются путем создания цепочки HTTP-запросов, как описано, может оказаться монолитные приложения, но его в соответствии с HTTP между процессами вместо механизмы intraprocess связи.

Таким образом для обеспечения автономности микрослужбу и повышения устойчивости, необходимо свести использование цепочек запросов и ответов взаимодействия между микрослужбами. Рекомендуется использовать только асинхронное взаимодействие для взаимодействия между микрослужбу, с помощью асинхронных сообщений и событий-связи на основе или с помощью HTTP-опросы независимо от исходного цикла запросов и ответов HTTP.

Объясняется использование асинхронное взаимодействие с дополнительными сведениями далее в этом руководстве в разделах [асинхронной микрослужбу принудительно автономность микрослужбу](#asynchronous-microservice-integration-enforce-microservices-autonomy) и [асинхронной связь на основе сообщений](#asynchronous-message-based-communication).

## <a name="additional-resources"></a>Дополнительные ресурсы

-   **Теорема CAP**
    [*https://en.wikipedia.org/wiki/CAP\_Теорема*](https://en.wikipedia.org/wiki/CAP_theorem)

-   **Итоговая согласованность**
    [*https://en.wikipedia.org/wiki/Eventual\_согласованности*](https://en.wikipedia.org/wiki/Eventual_consistency)

-   **Основные сведения о согласованности данных**
    [*https://msdn.microsoft.com/library/dn589800.aspx*](https://msdn.microsoft.com/library/dn589800.aspx)

-   **Мартин Фоулер (Martin Fowler). CQRS (команды и разделение ответственности запроса)**
    [*http://martinfowler.com/bliki/CQRS.html*](http://martinfowler.com/bliki/CQRS.html)

-   **Материализованные представления**
    [*https://docs.microsoft.com/azure/architecture/patterns/materialized-view*](https://docs.microsoft.com/azure/architecture/patterns/materialized-view)

-   **Чарльз строки. ACID vs. БАЗОВЫЙ: pH Shifting обработки транзакций базы данных**
    [*http://www.dataversity.net/acid-vs-base-the-shifting-ph-of-database-transaction-processing/*](http://www.dataversity.net/acid-vs-base-the-shifting-ph-of-database-transaction-processing/)

-   **Компенсирующие транзакции**
    [*https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction*](https://docs.microsoft.com/azure/architecture/patterns/compensating-transaction)

-   **UDI Dahan. Сервисноориентированные композиции**
    [*http://udidahan.com/2014/07/30/service-oriented-composition-with-video/*](http://udidahan.com/2014/07/30/service-oriented-composition-with-video/)


>[!div class="step-by-step"]
[Предыдущие] (логический и физического architecture.md) [Далее] (идентификации микрослужбу домена модели boundaries.md)
