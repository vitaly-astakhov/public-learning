# [Cache](https://www.rfc-editor.org/rfc/rfc9111)

**Cache** - это [опциональное](https://www.rfc-editor.org/rfc/rfc9111#:~:text=Although%20caching%20is%20an%20entirely%20OPTIONAL) локальное хранилище (**local store**) предыдущих ответных сообщений (**response messages**) и подсистема, управляющая хранением, извлечением и удалением сообщений. Кэш хранит кэшируемые ответы, чтобы сократить время отклика и потребление пропускной способности сети при будущих эквивалентных запросах.

Целью HTTP-кэширования является повышение производительности путем повторного использования предыдущего ответного (**response**) сообщения для удовлетворения текущего запроса.

## Cache types

Cache можно разбить на два типа:

###  Shared cache (общий кэш)

**Shared cache** - это кэш, в котором хранятся ответы для повторного использования более чем одним пользователем. Shared cache обычно, но не всегда, развертываются в составе посредника ([**intermediary** 📂](./intermediaries.md))

[Storing Responses to Authenticated Requests](https://www.rfc-editor.org/rfc/rfc9111#name-storing-responses-to-authen)

###  Private cache (частный кэш)

**Private cache (частный кэш)** - это кэш, который предназначен для одного пользователя. Часто они развертываются как компонент агента пользователя (**user agent**)

## Общее

**Cache key** - это идентификатор, который кэш использует для выбора ответа

Чаще всего в кэше хранится успешный ответ ([**200 OK**](https://www.rfc-editor.org/rfc/rfc9110.html#name-200-ok)) на запрос с методом `GET`, содержащий [представление целевого ресурсе](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.1). Однако также возможно сохранять перенаправления (**redirect**), отрицательные результаты (например, [404 Not Found](https://www.rfc-editor.org/rfc/rfc9110.html#name-404-not-found)), неполные результаты (например, [206 Partial Content](https://www.rfc-editor.org/rfc/rfc9110.html#name-206-partial-content)) и ответы на методы, отличные от `GET`.


Кэш считается отключенным (**disconnected**), когда он не может связаться с исходным сервером (**origin server**) или иным образом найти прямой путь для запроса.

___

## Что делает кэш

### Кэш сохраняет
- **Заголовки (headers)**
  - Кэш **ДОЛЖЕН** сохранять все поля заголовков (**header fields**), полученные вместе с ответом, при сохранении ответа. *(Есть [исключения из правил](https://www.rfc-editor.org/rfc/rfc9111#section-3.1-1))*.
  - Кэш **МОЖЕТ** как сохранять **trailer fields**, так и отбрасывать их, при сохранение ответа
  - Кэш **МОЖЕТ** сохранять [неполные ответы](https://www.rfc-editor.org/rfc/rfc9110#section-6.1), ответы с частичным содержимым ([**partial-content** 📂](./partial-content.md)), если они соблюдают [необходимые требования](https://www.rfc-editor.org/rfc/rfc9111#section-3.3-1). Ответы с частичным содержимым ([**partial-content** 📂](./partial-content.md)) так же могут быть объединены в один и повторно использовать этот ответ для удовлетворения последующих запросов, если все они используют один и тот же надежный валидатор ([**validator** 📂](./validation.md)) и кэш соответствует [требованиям клиента](https://www.rfc-editor.org/rfc/rfc9110#section-15.3.7.3).
  - Кэш **МОЖЕТ** хранить ответы на аутентифицированные запросы. [Подробнее](https://www.rfc-editor.org/rfc/rfc9111#name-storing-responses-to-authen)

### Кэш обновляет
- Кэш может [обновлять поля заголовков (**header fields**)](https://www.rfc-editor.org/rfc/rfc9111#section-3.2), уже сохраненного ответа (**response**) из другого (обычно более нового) в нескольких случаях:
  - [Combining Partial Content](https://www.rfc-editor.org/rfc/rfc9111#name-combining-partial-content)
  - [Freshening Stored Responses upon Validation](https://www.rfc-editor.org/rfc/rfc9111#name-freshening-stored-responses)
  - [Freshening Responses with HEAD](https://www.rfc-editor.org/rfc/rfc9111#name-freshening-responses-with-h)
- При начавшемся обновлении кэш **ДОЛЖЕН** добавить каждое поле заголовка из предоставленного ответа (обычно более нового) к сохраненному ранее ответу, заменив значения полей, которые уже присутствуют на новые. *Есть [исключения из правил](https://www.rfc-editor.org/rfc/rfc9111#section-3.2-2)*


___


## [Constructing Responses from Caches](https://www.rfc-editor.org/rfc/rfc9111#name-constructing-responses-from)


Чтобы ответ, находящийся в кэше, мог переиспользовать, **ДОЛЖНО** соблюдаться несколько условий:
- URI и метод ([**method**](./methods.md)) запроса должны быть идентичны тем, которые сохранены в кэше
- request header fields nominated by the stored response (if any) match those presented (see [Section 4.1](https://www.rfc-editor.org/rfc/rfc9111#caching.negotiated.responses)),
- Сохраненный ответ не содержит инструкцию `no-cache`
- Сохраненный ответ является одним из следующих:
  - ["свежим"](https://www.rfc-editor.org/rfc/rfc9111#expiration.model)
  - ["разрешается подавать несвежим"](https://www.rfc-editor.org/rfc/rfc9111#serving.stale.responses)
  - successfully validated (see [Section 4.3](https://www.rfc-editor.org/rfc/rfc9111#validation.model)).


### Request collapsing (Сворачивание запросов)

**Request collapsing** - Это практика, когда кэш может использовать сохраненный ответ для удовлетворения нескольких запросов, при условии, что разрешено повторно использовать этот ответ для соответствующих запросов. Это позволяет кэшу "сворачивать запросы" - или объединять несколько входящих запросов в один прямой запрос при сбое кэша - тем самым снижая нагрузку на исходный сервер и сеть.

Подробнее: [Fastly - Request collapsing](https://www.fastly.com/documentation/guides/concepts/edge-state/cache/request-collapsing/), [Cloudflare - Revalidation and request collapsing](https://developers.cloudflare.com/cache/concepts/revalidation/)


___

## Freshness

### Fresh (свежий)

Кэш считает сохраненный ответ «свежим», если его возраст еще не превысил срока его свежести и он может быть повторно использован без "валидации" ([**validation** 📂](./validation.md))

### Stale (Несвежий)

Кэш считает сохраненный ответ «несвежим», если его возраст уже превысил срока его свежести

Если кэшированный ответ не является свежим, он все равно может быть повторно использован, если проверка может обновить его или если источник проверяющего запроса недоступен.
