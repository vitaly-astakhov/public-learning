# Topics

### [Resources](https://www.rfc-editor.org/rfc/rfc9110#name-resources)
**Resources** - это то что хочет получить **User Agent** делая запрос (request) к **Original server**

### [Representations](https://www.rfc-editor.org/rfc/rfc9110#name-representations)
**Representations** - это разные формы конкретного ресурса (можно думать как о расширениях файлов). Например, одни и те же данные могут быть отформатированы как определенный тип носителя, такой как XML или JSON, локализованы для определенного письменного языка или географического региона и/или сжаты или иным образом закодированы для передачи. Базовый ресурс в каждом случае один и тот же, но его представление различается.
  [**Подробнее**](https://github.com/vitaliiastakhov/learning-private/issues/75#issuecomment-1964337871)

### [Clients, and Servers](https://www.rfc-editor.org/rfc/rfc9110#name-connections-clients-and-ser)
  - **Client** - это программа, которая устанавливает соединение с сервером с целью отправки одного или нескольких HTTP-запросов.
  - **Server** - это программа, которая принимает соединения для обслуживания HTTP-запросов путем отправки HTTP-ответов.

### [Messages 📂](./messages.md)

### [User Agent 📂](./user-agent.md)

### [Origin Server](https://www.rfc-editor.org/rfc/rfc9110#name-origin-server)
**Origin Server** - программа, которая может генерировать достоверные ответы (**response**) для получения целевого ресурса (**resource**). **Origin server** для URI "HTTP" идентифицируется компонентом [authority](https://www.rfc-editor.org/rfc/rfc9110#uri.references) [host:port] (www.example.com:443), который включает [идентификатор хоста](https://www.rfc-editor.org/rfc/rfc3986#section-3.2.2) и необязательный [номер порта](https://www.rfc-editor.org/rfc/rfc3986#section-3.2.3)

- **Примеры**: крупные общедоступные веб-сайты, устройства домашней автоматизации, настраиваемые сетевые компоненты, офисные машины, автономных роботов, новостные ленты, дорожные камеры, средства выбора рекламы в режиме реального времени и платформы видео по запросу
- **Header**: [Server](https://www.rfc-editor.org/rfc/rfc9110#name-server)

Из концепции **Origin Server** вытекает другая: [URI Origin](https://www.rfc-editor.org/rfc/rfc9110#name-uri-origin). URI Origin обязательно состоит из тройки: `scheme`, `host`, `port`. Два источника (**origin**) различны, если они отличаются чем либо из `scheme`, `host` или por`t.
Подробнее можно прочитать тут: [The Web Origin Concept](https://www.rfc-editor.org/rfc/rfc6454)

<!-- TODO: Поправить и, возможно, переместить дополнение про концепцию источника (origin), так как я не очень понял ее концепцию. И на тут выглядит как нагромождение. -->

### [Intermediaries 📂](./intermediaries.md)
### [Cache 📂](./cache.md) 📂
### [Status Codes 📂](./status-codes.md)

___


### [Representation Data 📂](./representation-data.md)
### [Web Origin 📂](./web-origin.md)
### [Content Negotiation 📂](./content-negotiation.md)
### [Conditional Requests 📂](./conditional-requests.md)
### [Partial Content 📂](./partial-content.md)
### [Headers Fields 📂](./headers-fields.md)
### [Validation 📂](./validation.md)
### [State Management (Cookie) 📂](./state-management-cookie.md)
### [CSP 📂](./csp.md)
### [Early Hints 📂](./early-hints.md)
### [Hints 📂](./hints.md)
