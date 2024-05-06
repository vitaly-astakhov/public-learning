# [Content negotiation](https://www.rfc-editor.org/rfc/rfc9110.html#section-12)

**Content negotiation (Согласование содержимого)** - это процесс, используемый HTTP-серверами для выбора оптимального представления ресурса, основываясь на предпочтениях клиента. Это позволяет серверу предоставлять различные версии одного и того же ресурса, например, на разных языках или в разных форматах.

## Предпочтения согласования содержимого (Content negotiation preferences)

Предпочтения согласования содержимого определяют, какие версии ресурса предпочтительнее для клиента. Эти предпочтения могут включать язык (`Accept-Language`), тип содержимого (`Accept`, `Accept-CH`), кодировку (`Accept-Encoding`) и другие параметры.

## Паттерны согласования содержимого (Content negotiation patterns)

- [**Проактивное согласование (Proactive negotiation aka Server-driven content negotiation)**](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.1): Сервер выбирает подходящее представление на основе предпочтений клиента, переданных в запросе, таких как `Accept`, `Accept-CH`, `Accept-CH-Lifetime`, `Accept-Language`, `Accept-Encoding`, `User-Agent`. Это позволяет серверу автоматически предоставлять наиболее подходящий контент.
- [**Реактивное согласование (Reactive Negotiation aka agent-driven negotiation)**](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.2): Клиент получает список доступных представлений и сам выбирает наиболее подходящее. Этот метод часто используется, когда сервер не может однозначно определить предпочтения клиента.
- [**Согласование содержимого запроса (Request Content Negotiation)**](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.3): Сервер может предоставить клиенту предпочтения для согласования содержимого, которые будут использоваться в последующих запросах. Это позволяет клиенту заранее знать, какие представления доступны и предпочтительны.

## Content Negotiation Fields

Если эти поля, отправляются (➡️) пользовательским агентом (**uses agent**), то они говорят о том, что ожидает получить пользователь.
Если эти поля, отправляются (⬅️) сервером, то они говорят о том, что ожидает получить сервер.

### [Accept](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.5.1)

**`Accept`** (🎩 ➡️ ⬅️)- это поле предоставляет информацию о предпочтительных *типах контента*.

Fetch API в алгоритме fetch [^1] определяет некоторые значение по-умолчанию для заголовка **`Accept`**, если это поле не было передано явно (*explicitly*), для некоторых направлений ([*destination*](https://fetch.spec.whatwg.org/#concept-request-destination)) запроса:

- `"document"`, `"frame"`, `"iframe"` - передается значение, которое равно `text/html,application/xhtml+xml,application/xml;q=0,9,*/*;q=0,8`. См: [*document Accept header value*](https://fetch.spec.whatwg.org/#document-accept-header-value)
- `"image"` - передается значение, которое равно `image/png,image/svg+xml,image/*;q=0.8,*/*;q=0.5`
- `"json"` - передается значение, которое равно `application/json,*/*;q=0.5`
- `"style"` - передается значение, которое равно `text/css,*/*;q=0.1`

### Accept-CH

### [Accept-Charset](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.5.2) 🎩 ➡️

### [Accept-Encoding](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.5.3) 🎩 ➡️⬅️

### [Accept-Language](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.5.4)

**`Accept-Language`** (🎩 ➡️⬅️) - Это поле предоставляет информацию о том, какие *языки* предпочтительными в содержании последующего запроса к тому же ресурсу

### [Vary](https://www.rfc-editor.org/rfc/rfc9110.html#section-12.5.5)

**`Vary`** (🎩 ⬅️) - Это поле предоставляет информацию о том какие поля, которые отвечают за согласования содержимого, ожидает увидеть сервер при последующем запросе.

**Пример**: `Vary: accept-encoding, accept-language`

[^1]: [Алгоритм fetch](https://fetch.spec.whatwg.org/#concept-fetch) шаг 13.
