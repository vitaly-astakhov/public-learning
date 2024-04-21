# Messaging

## [Server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#server-sent-events)

Чтобы серверы могли отправлять данные на веб-страницы по протоколу HTTP или с использованием выделенных серверных протоколов, в этой спецификации представлен интерфейс [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#eventsource).

Использование этого API заключается в создании объекта [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#eventsource) и регистрации прослушивателя событий (*event listener*).

Для работы с событиями, отправленные сервером (*server-sent events*) потребуется немного кода на сервере для потоковой передачи событий (*stream events*) во внешний интерфейс, но работа с клиентский кодом похоже на работу с websockets, в части обработки входящих событий, так как их интерфейс схож. Это одностороннее соединение, поэтому нельзя отправлять события с клиента на сервер.

[Примеры использования `EventSource` 📂](./examples/example-server-send-event.md)

## [Cross-document messaging](https://html.spec.whatwg.org/multipage/web-messaging.html#web-messaging)

## [Channel messaging](https://html.spec.whatwg.org/multipage/web-messaging.html#channel-messaging)
