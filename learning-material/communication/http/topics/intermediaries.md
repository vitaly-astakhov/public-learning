# [Intermediaries](https://www.rfc-editor.org/rfc/rfc9110#name-intermediaries)

## Materials

- <https://stackoverflow.com/questions/7155529/how-does-http-proxy-work>
- [Load Balancer и Reverse Proxy в микросервисной архитектуре](https://habr.com/ru/companies/otus/articles/741136/)
- [node-http-proxy](https://github.com/http-party/node-http-proxy)
- [http-proxy-middleware](https://github.com/chimurai/http-proxy-middleware)

___

**Intermediaries** - Мое слабое место. Не совсем понимаю какие концепции **proxy**, **gateway**, **tunnel**. Надо примеры их реализаций, для чего конкретно и абстрактно они могут быть использованы.
Подробнее: [Message Forwarding](https://www.rfc-editor.org/rfc/rfc9110#name-message-forwarding), [Message Transformations](https://www.rfc-editor.org/rfc/rfc9110#name-message-transformations)

- Туннели обычно используются для создания сквозного виртуального соединения, через один или несколько прокси-серверов, которые затем могут быть защищены с помощью [TLS](https://www.rfc-editor.org/rfc/rfc8446)
