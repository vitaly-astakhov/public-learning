# Navigation

Для работы с навигацией и историей сеансов HTML спецификация предлагает следующие API:

### [interface `Location`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#the-location-interface)

Это API предоставляет, помимо своих навигационных возможностей ([assign](https://html.spec.whatwg.org/multipage/nav-history-apis.html#dom-location-assign), [replace](https://html.spec.whatwg.org/multipage/nav-history-apis.html#dom-location-replace), [reload](https://html.spec.whatwg.org/multipage/nav-history-apis.html#dom-location-reload)), информацию об источнике (`origin`), и так же подробную информацию об URL (`protocol`, `host`, `port` и др.), который применим к текущему окну (`window`).

В настоящее время этот API для навигации разработчиками используется редко.

### [interface `History`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#the-history-interface)

### [interface `Navigation`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface)

#### Materials

- [Navigation API - [github]](https://github.com/WICG/navigation-api/blob/main/README.md)
- [The navigation API - [HTML Spec]](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-api)

___

В отличие от других навигационных API, `Navigation` API, помимо своих навигационных возможностей ([`navigate`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-navigate), [`reload`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-reload), [`back`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-back), [`forward`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-forward), [`traverseTo`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-traverseto)), предоставляет доступ к записям истории сеансов ([session history entries](https://html.spec.whatwg.org/multipage/browsing-the-web.html#session-history-entry)).

Записи истории сеансов предоставляются в виде объекта [**NavigationHistoryEntry**](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigationhistoryentry), который представляет только текущий навигационный объект ([*navigable*](https://html.spec.whatwg.org/multipage/document-sequences.html#navigable)), и, следовательно, на его содержимое не влияют навигация внутри навигационных контейнеров [(*navigable containers*)](https://html.spec.whatwg.org/multipage/document-sequences.html#navigable-container), таких как iframe, или навигация родительского навигационного объекта ([*parent navigable*](https://html.spec.whatwg.org/multipage/document-sequences.html#nav-parent)) в тех случаях, когда сам API навигации используется внутри iframe.

Кроме того, `Navigation` API содержит только объекты **NavigationHistoryEntry**, представляющие записи истории сеанса с тем же источником (**same-origin**), что и исходный, что означает, что если пользователь посещал другие источники до или после текущего, соответствующих **NavigationHistoryEntry** не будет.

Получить значения этого объекта **NavigationHistoryEntry** можно через аттрибуты `Navigation` API: [`entries`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-entries), [`currentEntry`,](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-currententry) [`activation`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#navigation-interface:dom-navigation-activation).

___

## Navigables and browsing contexts

### Navigable

Навигационные объекты (**navigables**) - это ориентированное на пользователя представление последовательности документов, т.е. они представляют собой нечто, по чему можно перемещаться между документами. Типичными примерами являются вкладки или окна в веб-браузере, или [iframes](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#the-iframe-element), или [frame](https://html.spec.whatwg.org/multipage/obsolete.html#frame) в [frameset](https://html.spec.whatwg.org/multipage/obsolete.html#frameset).

[Навигационный объект (**navigable**)](https://html.spec.whatwg.org/multipage/document-sequences.html#navigables) представляет `Document` пользователю через запись истории активного сеанса ([active session history entry](https://html.spec.whatwg.org/multipage/document-sequences.html#nav-active-history-entry)).

#### [Navigable target names](https://html.spec.whatwg.org/multipage/document-sequences.html#navigable-target-names)

Навигационным объектам (**navigable**) могут быть присвоены целевые имена ([*target names*](https://html.spec.whatwg.org/multipage/document-sequences.html#nav-target)), которые представляют собой строки, позволяющие определенным API (таким как `window.open()` или атрибут `target` элемента `<a/>`) настраивать навигацию по этому навигационному объекту (navigable).

Валидными целевыми именами для навигационных объектов считаются: `_blank`, `_self`, `_parent` `_top`.

### Traversable navigable

Проходимые навигационные объекты (**traversable navigables**) - это особый тип навигационных объектов, которые управляют историей сеансов самих себя и своих дочерних навигационных объектов.

Проходимый навигационный объект (**traversable navigables**) - это навигационный объект (**navigable**), который также управляет тем, какая запись истории сеанса должна быть текущей записью истории сеанса и активной записью истории сеанса для него самого и его дочерних навигационных объектов.

### Browsing context

Контексты просмотра (**browsing contexts**) - это ориентированное на разработчиков представление серии документов. Они соответствуют объектам [`WindowProxy`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#windowproxy) 1:1 (один к одному). Каждый навигационный объект (**navigable**) может представлять собой серию контекстов просмотра (**browsing contexts**), при этом [переключение](https://html.spec.whatwg.org/multipage/browsers.html#browsing-context-group-switches-due-to-cross-origin-opener-policy) между этими контекстами просмотра происходит при определенных четко определенных обстоятельствах.

A browsing context is a programmatic representation of a series of documents, multiple of which can live within a single navigable. Each browsing context has a corresponding WindowProxy object, as well as the following:

Контекст просмотра (**browsing context**) - это программное представление серии документов, несколько из которых могут находиться в пределах одного объекта навигации. Каждый контекст просмотра (**browsing context**) имеет соответствующий объект [WindowProxy](https://html.spec.whatwg.org/multipage/nav-history-apis.html#windowproxy), а также следующее другие концепции [описанные в спецификации](https://html.spec.whatwg.org/multipage/document-sequences.html#browsing-context)
