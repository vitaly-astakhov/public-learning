# [Links](https://html.spec.whatwg.org/multipage/links.html#links)

## Navigation

- [**`<link>`**](./doc-and-meta.md#link-element)
- [**`<a>`**](./text-elements.md#a-element)
- [Links created by `<a>` and `<area>` elements](#links-created-by-a-and-area-elements)

Ссылка (**link**) — это концептуальная конструкция, созданная элементами `<a>`, `<area>`, `<form>`, и `<link>`, которые представляют связь (*connection*) между двумя ресурсами, одним из которых является текущий документ.

## [Link types](https://html.spec.whatwg.org/multipage/links.html#linkTypes)

В HTML существует три типа ссылок:

- [ссылки на внешний ресурс (*links to external resources*)](https://html.spec.whatwg.org/multipage/links.html#external-resource-link) - это ссылки на ресурсы, которые будут использоваться для дополнения текущего документа, обычно автоматически обрабатываемые пользовательским агентом (*user agent*) и исполняются алгоритмом [fetch and process the linked resource](https://html.spec.whatwg.org/multipage/semantics.html#fetch-and-process-the-linked-resource).
- [гиперссылки (*hyperlinks*)](https://html.spec.whatwg.org/multipage/links.html#hyperlink) - это ссылки на другие ресурсы, которые обычно предоставляются пользователю агентом пользователя, чтобы пользователь мог заставить пользовательским агентом (*user agent*) перейти ([*navigate*](https://html.spec.whatwg.org/multipage/browsing-the-web.html#navigate)) к этим ресурсам, например, посетить их в браузере или загрузить их.
- [ссылки на внутренней ресурс (*internal resource links*)](https://html.spec.whatwg.org/multipage/links.html#internal-resource-link) - это ссылки на ресурсы в текущем документе, используемые для придания этим ресурсам особого значения или поведения.

Чтобы определить, какие типы ссылок применимы к элементу `<link>`, `<a>`, `<area>` или `<form>`, атрибут `rel` элемента должен быть разделен пробелами ([*split on ASCII whitespace*](https://infra.spec.whatwg.org/#split-on-ascii-whitespace)). Полученные маркеры являются ключевыми словами для типов ссылок, которые применяются к данному элементу.

Если не указано иное, ключевое слово не должно указываться более одного раза для каждого атрибута `rel`.

Ключевые слова, которые можно передать в аттрибут `rel` [представлены в таблице](https://html.spec.whatwg.org/multipage/links.html#table-link-relations). Все ключевые слова нечувствительны к регистру (*case-insensitive*).

### Resource hints keywords

Ключевые слова этого типа в аттрибуте `rel` используются только с элементом `<link>`.

#### [`dns-prefetch`](https://html.spec.whatwg.org/multipage/semantics.html#the-link-element:link-type-dns-prefetch)

Ключевое слово `dns-prefetch` указывает на то, что предварительное (*preemptively*) выполнение разрешения DNS для источника указанного ресурса, вероятно, будет полезным, поскольку весьма вероятно, что пользователю потребуются ресурсы, расположенные в этом источнике, и пользовательский опыт будет улучшен за счет предотвращения затрат на задержку, связанных с разрешением DNS.

#### [`preconnect`](https://html.spec.whatwg.org/multipage/links.html#link-type-preconnect)

Ключевое слово `preconnect` указывает на то, что предварительная инициализация подключения к источнику указанного ресурса, вероятно, будет полезной, поскольку весьма вероятно, что пользователю потребуются ресурсы, расположенные в этом источнике, и пользовательский опыт будет улучшен за счет предотвращения затрат на задержку, связанных с установлением соединения.

Пользовательский агент не должен задерживать событие загрузки ([*delay the load event*](https://html.spec.whatwg.org/multipage/parsing.html#delay-the-load-event)) для этого типа ссылок.

#### [`prefetch`](https://html.spec.whatwg.org/multipage/links.html#link-type-prefetch)

Ключевое слово `prefetch` указывает на то, что предварительная выборка (*preemptively* [*fetching*](https://fetch.spec.whatwg.org/#concept-fetch)) и кэширование указанного ресурса или документа на том же сайте, вероятно, будет полезным, поскольку весьма вероятно, что пользователю потребуется этот ресурс для будущих переходов.

#### [`preload`](https://html.spec.whatwg.org/multipage/links.html#link-type-preload)

Ключевое слово `preload` указывает, что пользовательский агент будет предварительно извлекать (*preemptively* [*fetch*](https://fetch.spec.whatwg.org/#concept-fetch)) и кэшировать указанный ресурс в соответствии с потенциальным пунктом назначения ([*potential destination*](https://fetch.spec.whatwg.org/#concept-potential-destination)), указанным атрибутом [`as`](https://html.spec.whatwg.org/multipage/semantics.html#attr-link-as), и приоритетом ([*priority*](https://fetch.spec.whatwg.org/#request-priority)), указанным атрибутом [`fetchpriority`](https://html.spec.whatwg.org/multipage/semantics.html#attr-link-fetchpriority), поскольку весьма вероятно, что пользователю потребуется этот ресурс для текущей навигации.

Пользовательский агент не должен задерживать событие загрузки ([*delay the load event*](https://html.spec.whatwg.org/multipage/parsing.html#delay-the-load-event)) для этого типа ссылок.

## Elements

### [Links created by `<a>` and `<area>` elements](https://html.spec.whatwg.org/multipage/links.html#links-created-by-a-and-area-elements)

> [!NOTE]
> Атрибут `href` для элементов **`<a>`** и **`<area>`** не требуется; если у этих элементов нет атрибутов href, они не создают гиперссылок [^1] и элементы **`<a>`** и **`<area>`** представляют собой заполнитель (*placeholder*) для места, где могла бы быть размещена ссылка. [^2]

Атрибут [`target`](https://html.spec.whatwg.org/multipage/links.html#attr-hyperlink-target), если он присутствует, должен быть допустимым для навигации целевым именем или ключевым словом ([*valid navigable target name or keyword*](https://html.spec.whatwg.org/multipage/document-sequences.html#valid-navigable-target-name-or-keyword)).

Атрибут [`download`](https://html.spec.whatwg.org/multipage/links.html#attr-hyperlink-download), если он присутствует, указывает на то, что автор намеревается использовать гиперссылку для загрузки ресурса.

Атрибут [`rel`](https://html.spec.whatwg.org/multipage/links.html#attr-hyperlink-rel) для элементов **`<a>`** и **`<area>`** определяет, какие типы связей создаются этими элементами. Атрибут `rel` элементов **`<a>`** и **`<area>`** поддерживает только следующие токены: [`noreferrer`](https://html.spec.whatwg.org/multipage/links.html#link-type-noreferrer), [`noopener`](https://html.spec.whatwg.org/multipage/links.html#link-type-noopener), и [`opener`](https://html.spec.whatwg.org/multipage/links.html#link-type-opener).

[^1]: [Источник](https://html.spec.whatwg.org/multipage/links.html#:~:text=The%20href%20attribute%20on%20a%20and%20area%20elements%20is%20not%20required)
[^2]: [Источник](https://html.spec.whatwg.org/multipage/text-level-semantics.html#:~:text=If%20the%20a%20element%20has%20no%20href%20attribute)
