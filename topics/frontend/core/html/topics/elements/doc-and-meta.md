# Document and metadata

## [`<head>` element](https://html.spec.whatwg.org/multipage/semantics.html#the-head-element)

Элемент **`<head>`** представляет собой набор метаданных для документа ([`Document`](https://html.spec.whatwg.org/multipage/dom.html#document)). И в себе может содержать следующие элементы: `<title>`, `<base>`, `<link>`, `<meta>`, `<style>`, `<script>`.

Некоторые элементы, которые находятся в элементе **`<head>`** могут [блокировать рендеринг](https://web.dev/learn/performance/understanding-the-critical-path#what_resources_are_on_the_critical_rendering_path) страницы документа HTML, до тех пор пока они не будут полностью загружены. К ним относятся `<style>`, `<script>` и `<link rel=stylesheet >`

### [`<title>` element](https://html.spec.whatwg.org/multipage/semantics.html#the-title-element) 🏷️

Элемент **`<title>`** представляет заголовок или имя документа. В одном документе должно быть не более одного элемента **`<title>`**. Значение элемента **`<title>`** можно получить через аттрибут документа [`document.title`](https://html.spec.whatwg.org/multipage/dom.html#document.title).

### [`<base>` element](https://html.spec.whatwg.org/multipage/semantics.html#the-base-element) 🏷️

Элемент **`<base>`** позволяет авторам указывать базовый URL-адрес документа для целей анализа URL-адресов и имя объекта навигации по умолчанию для перехода по гиперссылкам. Элемент не содержит никакого контента, кроме этой информации.

В одном документе должно быть не более одного элемента **`<base>`**. Элемент **`<base>`** должен иметь либо атрибут [`href`](https://html.spec.whatwg.org/multipage/semantics.html#dom-base-href), либо атрибут [`target`](https://html.spec.whatwg.org/multipage/semantics.html#dom-base-target), либо и то, и другое. Элемент **`<base>`**, если у него есть атрибут `href`, должен предшествовать любым другим элементам в дереве, атрибуты которых определены как принимающие URL-адреса.

### [`<link>` element](https://html.spec.whatwg.org/multipage/semantics.html#the-link-element) 🏷️ <a id="link-element"></a>

Элемент **`<link>`** позволяет авторам связать (***link***) документ с другими ресурсами.

Указать путь необходимого ресурса можно через аттрибуты [`href`](https://html.spec.whatwg.org/multipage/semantics.html#attr-link-href) и [`imagesrcset`](https://html.spec.whatwg.org/multipage/semantics.html#attr-link-imagesrcset).

Указать тип отношения (*relationship*), или связи, с ресурсом можно через атрибут `rel`, который, если он присутствует, должен содержать как минимум [один из разрешенных типов для этого аттрибута](https://html.spec.whatwg.org/multipage/links.html#linkTypes). Эти типы делятся на несколько категорий: [ссылка на внешний ресурс](https://html.spec.whatwg.org/multipage/links.html#external-resource-link), [гиперссылка](https://html.spec.whatwg.org/multipage/links.html#hyperlink), [ссылка на внутренней ресурс](https://html.spec.whatwg.org/multipage/links.html#internal-resource-link), подробнее можно узнать в [теме links 📂](./links.md).

Элемент **`<link>`** может создавать множество ссылок с разными категориями, которые перечисляются в аттрибуте `rel`. При этом, если элемент **`<link>`** не содержит аттрибут `rel`, тогда он не создает связь с необходимым ресурсом.

> [!NOTE]
> Гиперссылки, созданные с помощью элемента **`<link>`** и его атрибута `rel`, применяются ко всему документу в целом. Это контрастирует с атрибутом `rel` элементов `<a>` и `<area>`, который указывает тип ссылки, контекст которой задается расположением ссылки в документе.

### [`<meta>` element](https://html.spec.whatwg.org/multipage/semantics.html#the-meta-element) 🏷️

Элемент **`<meta>`** представляет различные виды метаданных, которые не могут быть выражены с помощью элементов `<title>`, `<base>`, `<link>`, `<style>` и `<script>`. Для элемента **`<meta>`** необходимо указать только один из атрибутов `name`, `http-equiv`, `charset` и `itemprop`. Если указано либо `name`, `http-equiv`, либо `itemprop`, то также должен быть указан атрибут `content`. В противном случае атрибут `content` должен быть опущен. Для атрибута `name` существует [несколько стандартных значений](https://html.spec.whatwg.org/multipage/semantics.html#standard-metadata-names), а также более расширенная версия, где присутствуют нестандартизированные имена, описанные в таблице [MetaExtensions [WHATWG]](https://wiki.whatwg.org/wiki/MetaExtensions).

### [`<style>` element](https://html.spec.whatwg.org/multipage/semantics.html#the-style-element) 🏷️

Элемент **`<style>`** позволяет авторам встраивать таблицы стилей CSS (*CSS style sheets*) в свои документы. Элемент **`<style>`** является одним из нескольких входных данных для модели обработки стилей. Этот элемент не представляет содержимое для пользователя.
