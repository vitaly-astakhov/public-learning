# Section elements

## [`<body>` element](https://html.spec.whatwg.org/multipage/sections.html#the-body-element)

Элемент `<body>` представляет содержимое (*contents*) документа. В документах должен быть только один элемент `<body>`.

Обработчики событий объекта `Window`, названные набором обработчиков событий элемента body, отображаемых в элементе `<body>` ([*Window-reflecting body element event handler set*](https://html.spec.whatwg.org/multipage/webappapis.html#window-reflecting-body-element-event-handler-set)), заменяют универсальные обработчики событий с теми же именами, которые обычно поддерживаются элементами HTML.

> [!IMPORTANT] Event handlers
> Обработчики событий объекта Window, которые отражаются в элементе body через набор обработчиков событий ([*Window-reflecting body element event handler set*](https://html.spec.whatwg.org/multipage/webappapis.html#window-reflecting-body-element-event-handler-set)), заменяют универсальные обработчики событий с теми же именами, которые обычно поддерживаются элементами HTML.
>
> То есть некоторые обработчики событий (*event handlers*) на элементе `<body>` следят за документом (`document`), а не за самим элементом body.

## [Sectioning content](https://html.spec.whatwg.org/multipage/dom.html#sectioning-content)

### [`<article>` element](https://html.spec.whatwg.org/multipage/sections.html#the-article-element)

Элемент `<article>` представляет собой полную или самостоятельную композицию в документе, странице, приложении или сайте и, в принципе, может распространяться независимо или повторно использоваться.

Элемент `<article>` может быть сообщением на форуме, статьей в журнале, записью в блоге, комментарием пользователя, интерактивным виджетом или любым другим независимым элементом контента.

Когда элементы `<article>` вложены, внутренние элементы `<article>` представляют `articles`, которые в принципе связаны с содержанием внешней статьи. Например, запись в блоге на сайте, который принимает комментарии, отправленные пользователем, может представлять комментарии как элементы `<article>`, вложенные в элемент `<article>` для записи в блоге. Эти записи могут содержаться в элементе `<section>`, как [показано в примере](https://html.spec.whatwg.org/multipage/sections.html#article-example).

### [`<section>` element](https://html.spec.whatwg.org/multipage/sections.html#the-section-element)

Элемент `<section>` представляет собой общий раздел документа или приложения. В данном контексте раздел представляет собой тематическую группу контента, обычно с заголовком (*heading*).

Примерами секций (`<section>`) могут быть главы, различные страницы с вкладками в диалоговом окне с вкладками или пронумерованные секции диссертации. Домашнюю страницу веб-сайта можно разделить на секции для введения, новостей и контактной информации.

> [!NOTE]
> Авторам рекомендуется использовать элемент `<article>` вместо элемента `<section>`, когда имеет смысл объединить содержимое элемента.
>
> [Источник](https://html.spec.whatwg.org/multipage/sections.html#:~:text=Authors%20are%20encouraged%20to%20use%20the)

### [`<nav>` element](https://html.spec.whatwg.org/multipage/sections.html#the-nav-element)

Элемент `<nav>` представляет собой раздел страницы, который ссылается на другие страницы или на части страницы: раздел с навигационными ссылками.

### [`<aside>` element](https://html.spec.whatwg.org/multipage/sections.html#the-aside-element)

Элемент `<aside>` представляет собой раздел страницы, содержащий содержимое (*content*), которое косвенно связано с содержимым, расположенным вокруг элемента `<aside>`, и которое можно рассматривать как отдельное от этого содержимого. Такие разделы часто представлены в виде боковых панелей (*sidebars*) в печатной типографии.

Элемент можно использовать для создания типографских эффектов, таких как выдвижные кавычки (*quotes*) или боковые панели (*sidebars*), для рекламы, для групп навигационных элементов (`<nav>`) и для другого контента, который считается отдельным от основного содержимого страницы.

## [Heading content](https://html.spec.whatwg.org/multipage/dom.html#heading-content)

### [heading elements (`<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`)](https://html.spec.whatwg.org/multipage/sections.html#the-h1,-h2,-h3,-h4,-h5,-and-h6-elements)

Эти элементы представляют собой заголовки соответствующих разделов.

Элементы `<h1>`–`<h6>` имеют уровень (*level*) заголовка, который задается числом в имени элемента.

#### Outline

Для элементов `<h1>`–`<h6>` HTML спецификации определяет такое понятие как структура (*outline*)

[**Outline**](https://html.spec.whatwg.org/multipage/sections.html#outline) - это все заголовки документа в древовидном порядке (*tree order*).

При этом, элементы заголовков, которые находятся в `<header>` не влияют на структуру (*outline*) документа.

[Примеры того как выглядит структура (**outline**)](https://html.spec.whatwg.org/multipage/sections.html#sample-outlines)

### [`<hgroup>` element](https://html.spec.whatwg.org/multipage/sections.html#the-hgroup-element)

Элемент `<hgroup>` представляет заголовок (*heading*) и связанный с ним контент. Элемент может использоваться для группировки элементов `<h1>`–`<h6>` с одним или несколькими элементами `<p>`, содержащими контент, представляющий подзаголовок, альтернативное название или слоган.

## Other section related elements

### [`<header>` element](https://html.spec.whatwg.org/multipage/sections.html#the-header-element)

Элемент `<header>` представляет собой группу вводных или навигационных средств.

> [!NOTE]
> A header element is intended to usually contain a heading (an h1–h6 element or an hgroup element), but this is not required. The header element can also be used to wrap a section's table of contents, a search form, or any relevant logos.
>
> The [`header`](https://html.spec.whatwg.org/multipage/sections.html#the-header-element) element is not [sectioning content](https://html.spec.whatwg.org/multipage/dom.html#sectioning-content-2); it doesn't introduce a new section.

### [`<footer>` element](https://html.spec.whatwg.org/multipage/sections.html#the-footer-element)

Элемент `<footer>` представляет собой нижний колонтитул для элемента содержимого раздела ([*sectioning content*](https://html.spec.whatwg.org/multipage/dom.html#sectioning-content-2)) ближайшего предка или для элемента `<body>`, если такого предка нет.

Элемент `<footer>` обычно содержит информацию о своем разделе, например, кто его написал (т.е. авторы сайта), ссылки на соответствующие документы, данные об авторских правах и тому подобное.

### [`<address>` element](https://html.spec.whatwg.org/multipage/sections.html#the-address-element)

Элемент `<address>` представляет контактную информацию для ближайшего к нему элемента `<article>` или элемента `<body>`. Если это элемент `<body>`, то контактная информация применяется ко всему документу в целом.

Элемент `<address>` не должен использоваться для представления произвольных адресов (например, почтовых адресов), если только эти адреса на самом деле не являются соответствующей контактной информацией. (Элемент `<p>` является подходящим элементом для обозначения почтовых адресов в целом.)

Элемент `<address>` не должен содержать информации, отличной от контактной информации.
