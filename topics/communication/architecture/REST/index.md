**REpresentational State Transfer (REST)** - архитектурный стиль, описывающий принципы разработки программного обеспечения, лежащие в основе **REST**, и ограничения (**restrictions**) взаимодействия, выбранные для сохранения этих принципов.

Эти ограничения в себя включают:

- Client-server model
- Statelessness
- Cache-ability
- Uniform interface
- Layered system
- Code-on-demand (optional)

Ограничения хорошо описаны в статье [Rethinking REST](https://kieranpotts.com/rethinking-rest#_the_rest_constraints).

**RESTful** - это веб-сервис или API, реализованный с использованием **HTTP** и принципов **REST**.

___

Главное, что определяет **REST**, это то что пользователь должен получать не ресурс (**resource**), а его представление (**representation**).

Компоненты **REST** выполняют действия с ресурсом (**resource**), используя представление (**representation**) для фиксации текущего или предполагаемого состояния этого ресурса и передачи этого представления (**representation**) между компонентами.

Представление (**representation**) состоит из данных (**data**), метаданных (**metadata**), описывающих данные, и, иногда, метаданных для описания метаданных (обычно с целью проверки целостности сообщения).

### [REST Data Elements](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#tab_5_1)

- **resource** - [**Resource [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.1)
- **resource identifier** - [**Identifiers in HTTP [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-4)
- **representation** - [**Representations [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.2)
- **representation metadata** - [**Representation Data and Metadata [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-8)
- **resource metadata** - [**Validator Fields [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#name-validator-fields)
- **control data** - [**Control Data [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#message.control.data)

### [REST Connectors](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#tab_5_2)

Соединители (**connectors**) представляют собой абстрактный интерфейс для взаимодействия [REST компонентов](/#REST%20Components), повышая простоту (**simplicity**) за счет четкого разделения задач и сокрытия базовой реализации ресурсов (**resources**) и механизмов связи. Поскольку соединитель (**connector**) управляет сетевым взаимодействием компонента, информация может распределяться между несколькими взаимодействиями, чтобы повысить эффективность и скорость реагирования.

- **client** - клиент инициирует связь, отправляя запрос (**request**) - [**Connections, Clients, and Servers [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.3)
- **server** - прослушивает соединения и отвечает на запросы (**request**), чтобы предоставить доступ к своим службам. - [**Connections, Clients, and Servers [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.3)
- **cache** - может быть расположен на интерфейсе клиентского или серверного соединителя для сохранения кэшируемых ответов на текущие взаимодействия, чтобы их можно было повторно использовать для последующих запрошенных взаимодействий. Кэш может использоваться клиентом (**client**), чтобы избежать повторения сетевого взаимодействия, или сервером (**server**), чтобы избежать повторения процесса генерации ответа, причем оба случая служат для уменьшения задержки взаимодействия. Некоторые соединители кэша являются общими (**shared**), что означает, что их кэшированные ответы могут использоваться в ответе клиенту, отличному от того, для которого ответ был первоначально получен. - [**Caches [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.8), [**HTTP Cache 📂**](../../http/topics/cache.md)
- **resolver** - преобразует частичные или полные идентификаторы ресурсов (**resource identifiers**) в информацию о сетевом адресе, необходимую для установления межкомпонентного соединения. Например, большинство URI включают имя хоста DNS в качестве механизма идентификации органа управления (**authority**) по именованию ресурса. Чтобы инициировать запрос, веб-браузер извлекает имя хоста из URI и использует преобразователь (**resolver**) DNS для получения адреса Интернет-протокола для этого органа управления (**authority**).
- **tunnel** - передает связь через границу соединения, такую как firewall или сетевой шлюз (*network gateway*) более низкого уровня. Единственная причина, по которой соединитель **tunnel** моделируется как часть **REST**, а не абстрагируется как часть сетевой инфраструктуры, заключается в том, что некоторые компоненты **REST** могут динамически переключаться с поведения активного компонента на поведение туннеля. - [**Intermediaries [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.7)

### [REST Components](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#tab_5_3)

Компонент может включать в себя как клиентские (**client**), так и серверные (**server**) соединители (**connector**).

- **origin server** - Исходный сервер (**origin server**) использует серверный соединитель (**server connector**) для управления пространством имен запрашиваемого ресурса. Он является окончательным источником представления (**representation**) своих ресурсов (**resources**) и должен быть конечным получателем любого запроса, направленного на изменение значения его ресурсов. - [**Origin Server [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.6)
- **intermediaries** - Промежуточные компоненты действуют как клиент (**client**), так и сервер (**server**) для пересылки запросов и ответов с возможным переводом. - [**Intermediaries [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.7), [**HTTP Intermediaries 📂**](../../http/topics/intermediaries.md)
  - **gateway (a.k.a., reverse proxy)** - это посредник (**intermediary**), устанавливаемый сетью (**network**) или исходным сервером (**origin server**) для обеспечения инкапсуляции интерфейса других служб для преобразования данных, повышения производительности или обеспечения безопасности.
  - **proxy** - это посредник (**intermediary**), выбранный клиентом (**client**) для обеспечения инкапсуляции интерфейса других служб, преобразования данных, повышения производительности или защиты безопасности.
- **user agent** - Пользовательский агент (**user agent**) использует клиентский соединитель (**client connector**) для инициирования запроса и становится конечным получателем ответа. - [**User Agents [HTTP Semantics]**](https://www.rfc-editor.org/rfc/rfc9110#section-3.5), [**HTTP User Agent 📂**](../../http/topics/user-agent.md)
