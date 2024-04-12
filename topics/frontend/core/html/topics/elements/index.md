### [Elements](https://html.spec.whatwg.org/multipage/dom.html#elements)

Термин «элементы HTML» относится к любому элементу в [**HTML namespace**](https://infra.spec.whatwg.org/#html-namespace).

Элементы, атрибуты и значения атрибутов в HTML определены (в соответствии с этой спецификацией) как имеющие определенные смыслы (**meanings**) (семантику).

Эти определения позволяют обработчикам HTML, таким как веб-браузеры или поисковые системы, представлять и использовать документы (**documents**) и приложения в самых разнообразных контекстах, которые автор, возможно, не рассматривал.

Поскольку HTML передает смысл (**meaning**), а не презентацию, та же страница может быть использована небольшим браузером на мобильном телефоне без каких-либо изменений на странице.

Полный список HTML элементов можно [найти здесь](https://html.spec.whatwg.org/multipage/indices.html#elements-3)

#### Elements Interfaces

- [Basic HTMLElement interface [HTML]](https://html.spec.whatwg.org/multipage/dom.html#htmlelement)
- [Interface Element [DOM]](https://dom.spec.whatwg.org/#element)
- [HTMLOrSVGElement interface [HTML]](https://html.spec.whatwg.org/multipage/dom.html#htmlorsvgelement)

### [Element definitions](https://html.spec.whatwg.org/multipage/dom.html#element-definitions)

Каждый элемент имеет определение, которое включает следующую информацию:

- [categories](https://html.spec.whatwg.org/multipage/dom.html#concept-element-categories) - [список категорий](https://html.spec.whatwg.org/multipage/dom.html#content-categories), к которым принадлежит элемент. Они используются при определении моделей контента для каждого элемента.
- [contexts in which this element can be used](https://html.spec.whatwg.org/multipage/dom.html#concept-element-contexts) - ненормативное описание того, где может использоваться элемент.
- [content model](https://html.spec.whatwg.org/multipage/dom.html#concept-element-content-model) - нормативное описание того, какой контент должен быть включен в качестве дочерних элементов и потомков данного элемента. [Контентом (*content*)](https://html.spec.whatwg.org/multipage/dom.html#concept-html-contents) элемента называют его дочерние элементы в DOM. Элементы без контента, но с пробелом обрабатываются пользовательскими агентами как нода `Text` в DOM.
- [tag omission in text/html](https://html.spec.whatwg.org/multipage/dom.html#concept-element-tag-omission) - Ненормативное описание того, можно ли в синтаксисе [`text/html`](https://html.spec.whatwg.org/multipage/iana.html#text/html)опускать начальный и конечный теги элемента.
- [content attributes](https://html.spec.whatwg.org/multipage/dom.html#concept-element-attributes) - нормативный список атрибутов, которые могут быть указаны в элементе (за исключением случаев, когда иное запрещено), вместе с ненормативными описаниями этих атрибутов. (Содержимое слева от тире является нормативным, содержимое справа от тире - нет.) У всех элементов имеются [**глобальные аттрибуты**](https://html.spec.whatwg.org/multipage/dom.html#global-attributes).
- [accessibility considerations](https://html.spec.whatwg.org/multipage/dom.html#concept-element-accessibility-considerations) - ссылки на ARIA спецификации для авторов и для разработчиков.
- [DOM interface](https://html.spec.whatwg.org/multipage/dom.html#concept-element-dom) - нормативное определение интерфейса DOM, которое должны реализовывать такие элементы.

Значение атрибута представляет собой строку. Если не указано иное, значения атрибутов элементов HTML могут быть любыми строковыми значениями, включая пустую строку, и нет никаких ограничений на то, какой текст может быть указан в таких значениях атрибутов.

#### [Kinds of content](https://html.spec.whatwg.org/multipage/dom.html#kinds-of-content)

- [metadata content](https://html.spec.whatwg.org/multipage/dom.html#metadata-content) - это контент, который определяет представление или поведение остального контента, или который устанавливает связь документа с другими документами, или который передает другую «внешнюю» информацию.
- [flow content](https://html.spec.whatwg.org/multipage/dom.html#flow-content) - это большинство элементов, используемых в основной части (*body*) документов и приложений
- [sectioning content](https://html.spec.whatwg.org/multipage/dom.html#sectioning-content) - это содержимое, определяющее область действия (*scope*) элементов `header` и `footer`.
- [heading content](https://html.spec.whatwg.org/multipage/dom.html#heading-content) - это содержимое, определяющее заголовок раздела.
- [phrasing content](https://html.spec.whatwg.org/multipage/dom.html#phrasing-content) - это текст документа, а также элементы, которые выделяют этот текст на уровне внутри абзаца.
  - [embedded content](https://html.spec.whatwg.org/multipage/dom.html#embedded-content-2) - это содержимое, которое импортирует в документ другой ресурс, или содержимое из другого словаря (*content from another vocabulary*)[^1], вставленное в документ.
- [interactive content](https://html.spec.whatwg.org/multipage/dom.html#interactive-content) - это контент, специально предназначенный для взаимодействия с пользователем.
- [palpable content](https://html.spec.whatwg.org/multipage/dom.html#palpable-content) - это содержимое, которое делает элемент непустым (*non-empty*), предоставляя либо некоторый непустой текст, либо что-то еще, что пользователи могут слышать (`audio` элементы) или просматривать (`video`, `img` или элементы `canvas`) или иным образом взаимодействовать (например, элементы управления интерактивной формой).
- [script-supporting elements](https://html.spec.whatwg.org/multipage/dom.html#script-supporting-elements) - это элементы, которые сами ничего не представляют (т.е. не отображаются), но используются для поддержки сценариев (*scripts*), например для обеспечения функциональности для пользователя.

Sectioning content, heading content, phrasing content, embedded content, interactive content - все это типы flow content. Метаданные (metadata) иногда являются flow content. Метаданные (metadata) и interactive content иногда являются phrasing content. Embedded content также является типом phrasing content, а иногда и interactive content.

[^1]: “content from another vocabulary” может означать использование элементов из других спецификаций, которые могут быть встроены в HTML-документ.  Например, [SVG](https://svgwg.org/svg2-draft/) и [MathML](https://w3c.github.io/mathml/)
