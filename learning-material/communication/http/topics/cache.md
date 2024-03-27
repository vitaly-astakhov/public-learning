# [Cache](https://www.rfc-editor.org/rfc/rfc9111)

**Cache** - это [опциональное](https://www.rfc-editor.org/rfc/rfc9111#:~:text=Although%20caching%20is%20an%20entirely%20OPTIONAL) локальное хранилище (**local store**) предыдущих ответных сообщений (**response messages**) и подсистема, управляющая хранением, извлечением и удалением сообщений. Кэш хранит кэшируемые ответы, чтобы сократить время отклика и потребление пропускной способности сети при будущих эквивалентных запросах.

Целью HTTP-кэширования является повышение производительности путем повторного использования предыдущего ответного (**response**) сообщения для удовлетворения текущего запроса.

## Cache types

Cache можно разбить на два типа:

### Shared cache (общий кэш)

**Shared cache** - это кэш, в котором хранятся ответы для повторного использования более чем одним пользователем. Shared cache обычно, но не всегда, развертываются в составе посредника ([**intermediary** 📂](./intermediaries.md))

[Storing Responses to Authenticated Requests](https://www.rfc-editor.org/rfc/rfc9111#name-storing-responses-to-authen)

### Private cache (частный кэш)

**Private cache (частный кэш)** - это кэш, который предназначен для одного пользователя. Часто они развертываются как компонент пользовательского агента (**user agent**)

## Общее

**Cache key** - это идентификатор, который кэш использует для выбора ответа

Чаще всего в кэше хранится успешный ответ ([**200 OK**](https://www.rfc-editor.org/rfc/rfc9110.html#name-200-ok)) на запрос с методом `GET`, содержащий [представление целевого ресурсе](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.1). Однако также возможно сохранять перенаправления (**redirect**), отрицательные результаты (например, [404 Not Found](https://www.rfc-editor.org/rfc/rfc9110.html#name-404-not-found)), неполные результаты (например, [206 Partial Content](https://www.rfc-editor.org/rfc/rfc9110.html#name-206-partial-content)) и ответы на методы, отличные от `GET`.

Кэш считается отключенным (**disconnected**), когда он не может связаться с исходным сервером (**origin server**) или иным образом найти прямой путь для запроса.

___

## Что делает кэш

### Кэш сохраняет

- **Заголовки (headers)**
  - Кэш **ДОЛЖЕН (MUST)** сохранять все поля заголовков (**header fields**), полученные вместе с ответом, при сохранении ответа. *(Есть [исключения из правил](https://www.rfc-editor.org/rfc/rfc9111#section-3.1-1))*.
  - Кэш **МОЖЕТ (MAY)** как сохранять **trailer fields**, так и отбрасывать их, при сохранение ответа
  - Кэш **МОЖЕТ (MAY)** сохранять [неполные ответы](https://www.rfc-editor.org/rfc/rfc9110#section-6.1), ответы с частичным содержимым ([**partial-content** 📂](./partial-content.md)), если они соблюдают [необходимые требования](https://www.rfc-editor.org/rfc/rfc9111#section-3.3-1). Ответы с частичным содержимым ([**partial-content** 📂](./partial-content.md)) так же могут быть объединены в один и повторно использовать этот ответ для удовлетворения последующих запросов, если все они используют один и тот же надежный валидатор ([**validator** 📂](./validation.md)) и кэш соответствует [требованиям клиента](https://www.rfc-editor.org/rfc/rfc9110#section-15.3.7.3).
  - Кэш **МОЖЕТ (MAY)** хранить ответы на аутентифицированные запросы. [Подробнее](https://www.rfc-editor.org/rfc/rfc9111#name-storing-responses-to-authen)

### Кэш обновляет

- Кэш может [обновлять поля заголовков (**header fields**)](https://www.rfc-editor.org/rfc/rfc9111#section-3.2), уже сохраненного ответа (**response**) из другого (обычно более нового) в нескольких случаях:
  - [При комбинировании частичного контента](https://www.rfc-editor.org/rfc/rfc9111#name-combining-partial-content)
  - [Freshening Stored Responses upon Validation](https://www.rfc-editor.org/rfc/rfc9111#name-freshening-stored-responses)
  - [Freshening Responses with HEAD](https://www.rfc-editor.org/rfc/rfc9111#name-freshening-responses-with-h)
- При начавшемся обновлении кэш **ДОЛЖЕН (MUST)** добавить каждое поле заголовка из предоставленного ответа (обычно более нового) к сохраненному ранее ответу, заменив значения полей, которые уже присутствуют на новые. *Есть [исключения из правил](https://www.rfc-editor.org/rfc/rfc9111#section-3.2-2)*

___

## [Constructing Responses from Caches](https://www.rfc-editor.org/rfc/rfc9111#name-constructing-responses-from)

Чтобы ответ, находящийся в кэше, мог переиспользовать, **ДОЛЖНО** соблюдаться несколько условий:

- URI и метод ([**method**](./methods.md) 📂) запроса должны быть идентичны тем, которые сохранены в кэше
- request header fields nominated by the stored response (if any) match those presented (see [Section 4.1](https://www.rfc-editor.org/rfc/rfc9111#caching.negotiated.responses)),
- Сохраненный ответ не содержит инструкцию `no-cache`
- Сохраненный ответ является одним из следующих:
  - ["свежим"](https://www.rfc-editor.org/rfc/rfc9111#expiration.model)
  - ["разрешается подавать несвежим"](https://www.rfc-editor.org/rfc/rfc9111#serving.stale.responses)
  - successfully validated (see [Section 4.3](https://www.rfc-editor.org/rfc/rfc9111#validation.model)).

### Request collapsing (Сворачивание запросов)

**Request collapsing** - Это практика, когда кэш может использовать сохраненный ответ для удовлетворения нескольких запросов, при условии, что разрешено повторно использовать этот ответ для соответствующих запросов. Это позволяет кэшу "сворачивать запросы" - или объединять несколько входящих запросов в один прямой запрос при сбое кэша - тем самым снижая нагрузку на исходный сервер и сеть.

Подробнее: [Fastly - Request collapsing](https://www.fastly.com/documentation/guides/topics/edge-state/cache/request-collapsing/), [Cloudflare - Revalidation and request collapsing](https://developers.cloudflare.com/cache/topics/revalidation/)

___

## [Freshness](https://www.rfc-editor.org/rfc/rfc9111#name-freshness)

Кэш считает сохраненный ответ *«свежим»*, если его возраст еще не превысил срока его свежести и он может быть повторно использован без "валидации" ([**validation** 📂](./validation.md))

Кэш считает сохраненный ответ *«несвежим»*, если его возраст уже превысил срока его свежести

Если кэшированный ответ не является свежим, он все равно может быть повторно использован, если проверка может обновить его или если источник проверяющего запроса недоступен.

**Срок свежести ответа (response's freshness lifetime)** - это промежуток времени между генерацией ответа исходным сервером (**origin server**) и истечением срока его действия.

Основным механизмом определения свежести является предоставление исходным сервером (**origin server**) явного срока службы ответа, используя либо поле заголовка [**`Expires`**](https://www.rfc-editor.org/rfc/rfc9111#name-expires) (раздел 5.3), либо директиву ответа [max-age](https://www.rfc-editor.org/rfc/rfc9111#name-max-age-2) в поле заголовка `Cache-Control`. Когда данные директивы присутствует более одного значения (например, две строки поля заголовка `Expires` или несколько директив `Cache-Control: max-age`), будет использовать либо первое вхождение, либо ответ следует считать устаревшим. Если директивы конфликтуют (например, присутствуют как `max-age`, так и `no-cache`), следует соблюдать наиболее ограничительную директиву.

При вычислении срока свежести ответа существует приоритет передаваемых полей и их директив. То есть, если какое-либо поле присутствует, freshness lifetime будет рассчитываться исходя из него. Порядок следующий: директива [`s-maxage`](https://www.rfc-editor.org/rfc/rfc9111#cache-response-directive.s-maxage), директива [`max-age`](https://www.rfc-editor.org/rfc/rfc9111#cache-response-directive.max-age), поле [`Expires`](https://www.rfc-editor.org/rfc/rfc9111#field.expires)

**Время истечения срока ответа (response's explicit expiration time)** - это время, в течение которого исходный сервер (**origin server**) предполагает, что сохраненный в кэше ответ больше не может использоваться кэшем без дальнейшей проверки.

**Возраст ответа (response's age)** - это время, которое прошло с момента как он был сгенерирован исходным сервером (**origin server**) или успешно проверен с его помощью. Предоставляется полем `Age`, [о нем ниже](#age).

Ответы с кодами состояния, которые определены как эвристически кэшируемые (например, [200](https://www.rfc-editor.org/rfc/rfc9110.html#name-200-ok), [203](https://www.rfc-editor.org/rfc/rfc9110.html#name-203-non-authoritative-infor), [204](https://www.rfc-editor.org/rfc/rfc9110.html#name-204-no-content), [206](https://www.rfc-editor.org/rfc/rfc9110.html#name-206-partial-content), [300](https://www.rfc-editor.org/rfc/rfc9110.html#name-300-multiple-choices), [301](https://www.rfc-editor.org/rfc/rfc9110.html#name-301-moved-permanently), [308](https://www.rfc-editor.org/rfc/rfc9110.html#name-308-permanent-redirect), [404](https://www.rfc-editor.org/rfc/rfc9110.html#name-404-not-found), [405](https://www.rfc-editor.org/rfc/rfc9110.html#name-405-method-not-allowed), [410](https://www.rfc-editor.org/rfc/rfc9110.html#name-410-gone), [414](https://www.rfc-editor.org/rfc/rfc9110.html#name-414-uri-too-long) и [501](https://www.rfc-editor.org/rfc/rfc9110.html#name-501-not-implemented)), могут быть повторно использованы кэшем с эвристическим сроком действия. если иное не указано в определении метода или явных элементах управления кэшем; все остальные коды состояния не подлежат эвристическому кэшированию.

## [Validation](https://www.rfc-editor.org/rfc/rfc9111#section-4.3)

Когда кэш не может выбрать для запроса сохраненный ответ, например по причине того, что ответ уже не считается свежим, кэш может использовать механизм условного запроса ([**conditional request** 📂](./conditional-requests.md)), делая запрос к исходному серверу (**origin server**), чтобы дать ему возможность выбрать действительный сохраненный ответ для использования, обновить сохраненные метаданные в процессе или заменить сохраненный ответ(ы) новым ответом. Этот процесс известен как "validating (проверка)" или "revalidating (повторная проверка)" сохраненного ответа.

При генерации условного запроса (**conditional request**) для валидации кэш либо запускается с запроса, который он пытается удовлетворить, либо синтезирует запрос, используя сохраненный ответ, копируя поля метода, целевого URI и заголовков запроса, идентифицируемые полем заголовка Vary

Затем получатели (**recipients**) сравнивают поля заголовка предварительного условия (**precondition**), чтобы определить, эквивалентен ли какой-либо сохраненный ответ текущему представлению ресурса

Если кэш получает запрос, который может быть удовлетворен путем повторного использования сохраненного ответа [`200 (OK)`](https://www.rfc-editor.org/rfc/rfc9110#status.200) или [`206 (Partial Content)`](https://www.rfc-editor.org/rfc/rfc9110#status.206), кэш **ДОЛЖЕН (SHOULD )** оценить любые применимые предварительные условия условного поля заголовка, полученные в этом запросе, в отношении соответствующих средств проверки, содержащихся в сохраненном ответе.

Правильная оценка кэшем условных запросов (**conditional requests**) зависит от полученных полей заголовка предварительного условия (**precondition**) и их приоритета. Таким образом, поля условного заголовка `If-Match` и `If-Unmodified-Since` неприменимы к кэшу, а `If-None-Match`имеет приоритет над `If-Modified-Since`. [Подробнее можно ознакомиться тут](https://www.rfc-editor.org/rfc/rfc9110#section-13.2.2).

Кэш **обрабатывает ответ на условный запрос** в зависимости от его кода состояния:

- Код состояния ответа [`304 (Not Modified)`](https://www.rfc-editor.org/rfc/rfc9110#status.304) указывает на то, что сохраненный ответ может быть обновлен и повторно использован
- Полный ответ (т.е. содержащий содержимое) указывает на то, что ни один из сохраненных ответов, указанных в условном запросе, не подходит. Вместо этого кэш **ДОЛЖЕН (MUST)** использовать полный ответ для удовлетворения запроса. Кэш МОЖЕТ хранить такой полный ответ с учетом [его ограничений](https://www.rfc-editor.org/rfc/rfc9111#response.cacheability).
- Если кэш получает ответ [`5xx (Server Error`)](https://www.rfc-editor.org/rfc/rfc9110#name-server-error-5xx) при попытке проверки ответа, он может либо переслать этот ответ запрашивающему клиенту, либо действовать так, как если бы сервер не смог ответить. В последнем случае кэш может отправить ранее сохраненный ответ, с учетом его [ограничений на это](https://www.rfc-editor.org/rfc/rfc9111#serving.stale.responses), или повторить запрос на проверку

Когда кэш отправляет входящий запрос `HEAD` для целевого URI и получает ответ [`200 (OK)`](https://www.rfc-editor.org/rfc/rfc9110#status.200), кэш **ДОЛЖЕН (SHOULD)** обновить или аннулировать (**invalidate**) каждый из своих сохраненных ответов `GET`, которые могли быть выбраны для этого запроса.

## [Invalidation](https://www.rfc-editor.org/rfc/rfc9111#section-4.4)

**Invalidation (аннулирование)** означает, что кэш может либо удалить все сохраненные ответы, целевой URI которых соответствует заданному URI, либо пометить их как "недействительные (**invalid**)" и нуждающиеся в обязательной проверке (**validation**), прежде чем они смогут быть отправлены в ответ на последующий запрос.

Кэш **ДОЛЖЕН (MUST)** аннулировать целевой URI, когда он получает <u>код состояния без ошибки</u> ([2xx (Successful)](https://www.rfc-editor.org/rfc/rfc9110#name-successful-2xx) или [3xx (Redirection)](https://www.rfc-editor.org/rfc/rfc9110#name-redirection-3xx)) в ответ на небезопасный метод (например: `POST`, `PATCH`, `PUT`, or `DELETE`) запроса (включая методы, безопасность которых неизвестна).

## Поля

### Age 🎩 ⬅️

- [**Age**](https://www.rfc-editor.org/rfc/rfc9111#section-4.2.3) - это поле передает оценку отправителем времени с момента создания ответа или его успешной проверки на исходном сервере.
- **Использование**: это поле используется для передачи приблизительного (просчитанного) возраста ответного сообщения, полученного из кэша. Значение поля *Age* - это оценка кэшем количества неотрицательных (**non-negative**) секунд, прошедших с тех пор, как исходный сервер сгенерировал или подтвердил (**validate**) ответ. Подробнее про то как возраст ответа оценивается можно [прочитать здесь](https://www.rfc-editor.org/rfc/rfc9111#name-calculating-age)

### [Cache-Control](https://www.rfc-editor.org/rfc/rfc9111#name-cache-control) 🎩 ➡️ ⬅️

- **Cache-Control** - это поле которое содержит директивы (инструкции) которые управляют кэшированием в браузерах и общими кэшами (**shared cashes**) (например, прокси, CDN).
- **Использование**: это поле используется для перечисления директив для кэшей по цепочке запросов/ответов

Полный список зарегистрированных директив: <https://www.iana.org/assignments/http-cache-directives/http-cache-directives.xhtml>

[**Request Directives**](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1):

- [`max-age`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.1) - эта директива указывает, что клиент предпочитает ответ, срок действия которого меньше или равен указанному количеству секунд. Если также не присутствует директива запроса `max-stale`, клиент не желает получать устаревший ответ.
- [`max-stale`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.2) - эта директива указывает, что клиент примет ответ, срок действия которого превысил срок его свежести. Если присутствует значение, то клиент готов принять ответ, срок действия которого превысил срок его свежести не более чем на указанное количество секунд. Если `max-stale` не присвоено значение, то клиент примет устаревший ответ любого возраста (поле `Age`).
- [`min-fresh`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.3) - эта директива указывает, что клиент предпочитает ответ, срок свежести которого не меньше его текущего возраста (поле `Age`) плюс, указанное в этом поле, время в секундах. То есть клиент хочет, чтобы ответ оставался свежим по крайней мере в течение указанного количества секунд.
- [`no-cache`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.4) - эта директива указывает, что клиент предпочитает, чтобы сохраненный ответ не использовался для удовлетворения запроса без успешной проверки на исходном сервере.
  - Поскольку многие старые реализации кэша (HTTP/1.0) не поддерживают директиву `no-cache`, можно использовать директиву `max-age` со значение 0, т.е. `max-age=0`
- [`no-store`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.5) - эта директива указывает, что кэш **НЕ ДОЛЖЕН** хранить какую-либо часть ни этого запроса, ни какого-либо ответа на него. Эта директива применяется как к частным, так и к общим кэшам.
- [`no-transform`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.6) - эта директива указывает на то, что клиент обращается к посредникам ([**intermediaries** 📂](./intermediaries.md)) с просьбой избежать преобразования контента.
- [`only-if-cached`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.1.7) - эта директива указывает, что клиент желает получить только сохраненный ответ. Кэши, выполняющие эту директиву запроса, должны при ее получении отвечать либо сохраненным ответом, соответствующим другим ограничениям запроса, либо кодом состояния 504 (тайм-аут шлюза).

**Квалифицированная форма (qualified form) директивы** - это директива, которая содержит один или несколько аргументов (#field-name).

<!-- TODO: Не совсем понимаю смысл и зачем использовать эти поля и используются ли они вообще -->

Квалифицированная форма директивы часто обрабатывается кэшами так, как если бы была получена неквалифицированная директива без кэширования; то есть специальная обработка для квалифицированной формы широко не реализована.

[**Response Directives**](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2):

- [`max-age`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.1) - эта директива указывает, что ответ должен считаться устаревшим после того, как его возраст превысит указанное в этой директиве количество секунд.
- [`must-revalidate`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.2) - эта директива указывает, что как только ответ устарел (**stale**), кэш **НЕ ДОЛЖЕН** повторно использовать этот ответ для удовлетворения другого запроса до тех пор, пока он не будет [успешно проверен источником](https://www.rfc-editor.org/rfc/rfc9111#validation.model).
- [`must-understand`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.3) - эта директива ограничивает кэширование ответа кэшем, который понимает и соответствует требованиям к коду состояния этого ответа, то есть, ответ кэшируется только в том случае, если кэш поддерживает семантику кода состояния ( **status code**). В целях отката (**fallback**) эту директиву `must-understand` рекомендуется использовать в сочетании с **`no-store`** в случае, если директива `must-understand` не поддерживается кэшем и, следовательно, игнорируется. Подробнее: [источник 1](https://www.rfc-editor.org/rfc/rfc9110#section-16.2.2-6), [источник 2](https://stackoverflow.com/questions/77318595/cache-control-i-dont-understand-must-understand), [источник 3](https://blog.jxck.io/entries/2021-02-12/cache-control-must-understand.html).
- [`no-cache`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.4) -
  - эта директива в ее неквалифицированной форме (без аргумента) указывает, что ответ **НЕ ДОЛЖЕН** использоваться для удовлетворения любого другого запроса без отправки его на проверку (**validation**) и получения успешного ответа. Это позволяет исходному серверу (**origin server**) запретить кэшу использовать ответ для удовлетворения запроса, не связываясь с ним, даже с помощью кэшей, которые были настроены на отправку устаревших ответов.
  - The qualified form of the no-cache response directive, with an argument that lists one or more field names, indicates that a cache MAY use the response to satisfy a subsequent request, subject to any other restrictions on caching, if the listed header fields are excluded from the subsequent response or the subsequent response has been successfully revalidated with the origin server (updating or removing those fields). This allows an origin server to prevent the reuse of certain header fields in a response, while still allowing caching of the rest of the response.
- [`no-store`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.5) - эта директива указывает, что кэш **НЕ ДОЛЖЕН** хранить какую-либо часть ни непосредственного запроса, ни ответа и **НЕ ДОЛЖЕН** использовать ответ для удовлетворения любого другого запроса
- [`no-transform`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.6) - директива указывает, что посредник (независимо от того, реализует ли он кэш) **НЕ ДОЛЖЕН** преобразовывать содержимое.
- [`private`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.7)
  - Если директива *unqualified*, то эта директива указывает, что общий (**shared**) кэш **НЕ ДОЛЖЕН** хранить ответ
  - The unqualified private response directive indicates that a shared cache MUST NOT store the response (i.e., the response is intended for a single user). It also indicates that a private cache MAY store the response, subject to the constraints defined in [Section 3](https://www.rfc-editor.org/rfc/rfc9111#response.cacheability), even if the response would not otherwise be heuristically cacheable by a private cache
  - If a qualified private response directive is present, with an argument that lists one or more field names, then only the listed header fields are limited to a single user: a shared cache MUST NOT store the listed header fields if they are present in the original response but MAY store the remainder of the response message without those header fields, subject the constraints defined in [Section 3](https://www.rfc-editor.org/rfc/rfc9111#response.cacheability).
- [`proxy-revalidate`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.8) - эта директива указывает, что как только ответ устарел (**stale**), общий (**shared**) кэш **НЕ ДОЛЖЕН** повторно использовать этот ответ для удовлетворения другого запроса до тех пор, пока он не будет успешно проверен источником
- [`public`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.9) - эта директива указывает, что кэш **МОЖЕТ (MAY)** хранить ответ, даже если в он был бы запрещен, [с учетом ограничений](https://www.rfc-editor.org/rfc/rfc9111#response.cacheability). Другими словами, public явно помечает ответ как кэшируемый. Например, public позволяет общему кэшу повторно использовать ответ на запрос, содержащий поле заголовка [`Authorization`](https://www.rfc-editor.org/rfc/rfc9111#caching.authenticated.responses).
- [`s-maxage`](https://www.rfc-editor.org/rfc/rfc9111#section-5.2.2.10) - эта директива указывает, что для общего кэша (**shared cache**) максимальный возраст, указанный этой директивой, переопределяет максимальный возраст, указанный либо директивой `max-age`, либо полем заголовка `Expires`. Общий кэш **НЕ ДОЛЖЕН** повторно использовать устаревший ответ с помощью s-maxage для удовлетворения другого запроса, пока он не будет успешно проверен источником

### [Expires](https://www.rfc-editor.org/rfc/rfc9111#name-expires) 🎩⬅️

**Expires** - это поле указывает дату/время, после которого ответ считается устаревшим (**stale**). Если ответ содержит поле заголовка `Cache-Control` с одну из следующих директив: `max-age`, `s-maxage`, получатель **ДОЛЖЕН (MUST)** игнорировать поле заголовка `Expires`.

### Pragma 🎩➡️👎

**Pragma** - это устаревшее поле, которое в качестве значения использовал директиву **"no-cache"** и в следствии обновления архитектуры работы с кешем (появление поля **Cache-Control**), это поле стало использоваться меньше. Иногда используется в целях отката (**fallback**) для протокола HTTP/1.0. Можно встретить это поле включая функции "Disable cache" в DevTools.

___

Приложения, использующие HTTP, часто указывают дополнительные формы кэширования. Например, веб-браузеры часто имеют [механизмы истории](https://developer.mozilla.org/en-US/docs/Web/API/History_API), такие как кнопки «Назад», которые можно использовать для повторного отображения представления, полученного ранее в сеансе.

Аналогично, некоторые веб-браузеры реализуют кэширование изображений и других ресурсов при просмотре страницы; они могут соблюдать или не соблюдать семантику HTTP-кэширования.

Требования [спецификации HTTP Caching](https://www.rfc-editor.org/rfc/rfc9111) не обязательно применяются к тому, как приложения используют данные после их получения из кэша HTTP. Например, [механизм истории](https://developer.mozilla.org/en-US/docs/Web/API/History_API) может отображать предыдущее представление, даже если срок его действия истек, а приложение может использовать кэшированные данные другими способами, выходящими за рамки срока их актуальности.

[Спецификация HTTP Caching](https://www.rfc-editor.org/rfc/rfc9111) не запрещает приложению учитывать кэширование HTTP; например, механизм истории может сообщать пользователю, что представление устарело, или он может выполнять директивы кэша (например, Cache-Control: no-store).
