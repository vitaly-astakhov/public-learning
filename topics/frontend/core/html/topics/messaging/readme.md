# Messaging

## Table of contents

- [Overview](#overview)
- [Server-sent events](#server-sent-events)
- [Cross-document messaging](#cross-document-messaging)
  - [Cross-document messaging security](#cross-document-messaging-security)
- [Channel messaging](#channel-messaging)
- [Broadcasting to other browsing contexts](#broadcasting-to-other-browsing-contexts)

## Overview

Сообщения в событиях, отправляемых сервером ([*server-sent events*](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events)), междокументных сообщениях ([*cross-document messaging*](https://html.spec.whatwg.org/multipage/web-messaging.html#web-messaging)), канальных сообщениях ([*channel messaging*](https://html.spec.whatwg.org/multipage/web-messaging.html#channel-messaging)), [broadcast channels](https://html.spec.whatwg.org/multipage/web-messaging.html#broadcasting-to-other-browsing-contexts) и [WebSockets](https://websockets.spec.whatwg.org/) используют интерфейс [`MessageEvent`](https://html.spec.whatwg.org/multipage/comms.html#messageevent) для своих событий сообщений (*[message](https://html.spec.whatwg.org/multipage/indices.html#event-message) events*)

## [Server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events)

Чтобы серверы могли отправлять данные на веб-страницы по протоколу HTTP или с использованием выделенных серверных протоколов, в этой спецификации представлен интерфейс [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#eventsource).

Использование этого API заключается в создании объекта [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#eventsource) и регистрации прослушивателя событий (*event listener*).

Для работы с событиями, отправленные сервером (*server-sent events*) потребуется немного кода на сервере для потоковой передачи событий (*stream events*) во внешний интерфейс, но работа с клиентский кодом похоже на работу с websockets, в части обработки входящих событий, так как их интерфейс схож. Это одностороннее соединение, поэтому нельзя отправлять события с клиента на сервер.

[Примеры использования `EventSource` 📂](./examples/example-server-send-event.md)

## [Cross-document messaging](https://html.spec.whatwg.org/multipage/web-messaging.html#web-messaging)

Веб-браузеры по соображениям безопасности и конфиденциальности не позволяют документам в разных доменах влиять друг на друга, то есть межсайтовый скриптинг (*cross-site scripting*) запрещен.

Хотя это важная функция безопасности, она предотвращает взаимодействие страниц из разных доменов, даже если эти страницы не являются враждебными. Но существует система обмена сообщениями (*messaging system*), которая позволяет документам обмениваться данными друг с другом независимо от их исходного домена, таким образом, чтобы исключить возможность межсайтовых скриптовых атак.

Использовать систему обмена сообщениями (*messaging system*) можно через метод `[window.postMessage()](https://html.spec.whatwg.org/multipage/web-messaging.html#dom-window-postmessage-options)`, который отправляет сообщение в указанное окно. Сообщения могут быть структурированными объектами (*structured objects*), например вложенными объектами и массивами, могут содержать значения JavaScript (строки, числа, объекты даты (*`[Date](https://tc39.es/ecma262/#sec-date-objects)` objects*) и т.д.) и могут содержать определенные объекты данных.

### Cross-document messaging security

Авторам следует проверить атрибут `origin`, чтобы убедиться, что сообщения принимаются только с тех доменов, с которых они ожидают получать сообщения. В противном случае ошибки в авторском коде обработки сообщений могут быть использованы враждебными (*hostile*) сайтами.

Кроме того, даже после проверки атрибута `origin` авторы должны также убедиться, что данные, о которых идет речь, соответствуют ожидаемому формату. В противном случае, если источник события был атакован с использованием ошибки межсайтового скриптинга, дальнейшая неконтролируемая обработка информации, отправленной с использованием метода `postMessage()`, может привести к распространению атаки на получателя.

Авторам не следует использовать ключевое слово с подстановочным (*wildcard*) знаком (*) в аргументе [`targetOrigin`](https://html.spec.whatwg.org/multipage/web-messaging.html#dom-window-postmessage) в сообщениях, содержащих какую-либо конфиденциальную информацию, поскольку в противном случае невозможно гарантировать, что сообщение будет доставлено только тому получателю, которому оно предназначалось.

Авторам, принимающим сообщения от любого источника, рекомендуется учитывать риски, связанные с атакой типа "отказ в обслуживании" ("*denial-of-service*"). Злоумышленник может отправить большое количество сообщений; если принимающая страница выполняет дорогостоящие вычисления или вызывает отправку сетевого трафика для каждого такого сообщения, сообщение злоумышленника может быть преобразовано в атаку типа "отказ в обслуживании". Авторам рекомендуется использовать ограничение скорости (принимать только определенное количество сообщений в минуту), чтобы сделать такие атаки непрактичными.

## [Channel messaging](https://html.spec.whatwg.org/multipage/web-messaging.html#channel-messaging)

Чтобы обеспечить прямую связь независимых фрагментов кода (например, выполняющихся в разных контекстах просмотра (*browsing contexts*)), авторы могут использовать обмен сообщениями по каналам ([*channel messaging*](https://html.spec.whatwg.org/multipage/web-messaging.html#channel-messaging)).

Каналы связи (*communication channels*) в этом механизме реализованы в виде двухсторонних каналов с портом на каждом конце. Сообщения, отправленные через один порт, доставляются на другой порт, и наоборот. Сообщения доставляются как события DOM, не прерывая и не блокируя выполнение [задач](https://html.spec.whatwg.org/multipage/webappapis.html#concept-task).

Обмен сообщениями по каналам ([*channel messaging*](https://html.spec.whatwg.org/multipage/web-messaging.html#channel-messaging)) происходит после создания канала [`MessageChannel`](https://html.spec.whatwg.org/multipage/web-messaging.html#messagechannel) на основе портов [`MessagePort`](https://html.spec.whatwg.org/multipage/web-messaging.html#messageport), которые при объявлении возвращает [`MessageChannel`](https://html.spec.whatwg.org/multipage/web-messaging.html#messagechannel).

[Примеры использования `MessageChannel` 📂](./examples/example-channel-messaging.md)

## [Broadcasting to other browsing contexts](https://html.spec.whatwg.org/multipage/web-messaging.html#broadcasting-to-other-browsing-contexts)

Страницы, которые открыты в одном источнике (*origin*), одним и тем же пользователем в одном и том же пользовательском агенте (*user agent*), но в разных, не связанных между собой контекстах просмотра ([*browsing contexts*](https://html.spec.whatwg.org/multipage/document-sequences.html#browsing-context)), иногда нуждаются в отправке уведомлений друг другу, например "hey, the user logged in over here, check your credentials again".

Для сложных случаев, например, для управления блокировкой общего состояния, для управления синхронизацией ресурсов между сервером и несколькими локальными клиентами, для совместного использования соединения `WebSocket` с удаленным хостом и т.д., общие рабочие системы ([*shared workers*](https://html.spec.whatwg.org/multipage/workers.html#sharedworker)) являются наиболее подходящим решением.

Однако для простых случаев, когда общий рабочий процесс ([*shared workers*](https://html.spec.whatwg.org/multipage/workers.html#sharedworker)) может привести к неоправданным накладным расходам, авторы могут использовать простой механизм вещания на основе каналов (*channel-based broadcast mechanism*).

Использовать механизм вещания на основе каналов можно через интерфейс [`BroadcastChannel`](https://html.spec.whatwg.org/multipage/web-messaging.html#broadcastchannel), с помощью которого могут отправляться и приниматься сообщения для данного названия канала.

[Примеры использования `BroadcastChannel` 📂](./examples/example-broadcast-channel.md)
