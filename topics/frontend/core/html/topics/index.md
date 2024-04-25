# HTML

Семантикой (**semantic**) в HTML называется содержание/смысл/значение (*meaning*).

___

## Window

### Materials

- [Defining the WindowProxy, Window, and Location objects](https://blog.whatwg.org/windowproxy-window-and-location)

___

Объект `window` в HTML представляет собой глобальный объект, который служит точкой входа в `DOM` (Document Object Model) связанного документа [`Document 📂`](./document.md) и предоставляет функциональность на уровне браузера, такую как навигация по истории и многое другое.

Контекст просмотра объекта `Window` - это контекст просмотра связанного с ним документа [`Document 📂`](./document.md).

Контекст объекта можно получить через `window` так же можно получить через глобальное свойство [`globalThis`](https://tc39.es/ecma262/multipage/global-object.html#sec-globalthis).

### Window interfaces

- [Window - [HTML]](https://html.spec.whatwg.org/multipage/nav-history-apis.html#window)

___

### [Plugins](https://html.spec.whatwg.org/multipage/infrastructure.html#plugins)

Плагинами в HTML спецификации называются используемые и регулируемые пользовательским агентом обработчики контента, которые расширяют стандартные функции пользовательского агента.

Примеры таких плагинов:

- [PDF viewer](https://html.spec.whatwg.org/multipage/system-state.html#pdf-viewing-support)

Узнать какие плагины можно было через `window.navigator.plugins`. Сейчас аттрибут `plugins` считается устаревшим (*deprecated*).

<!-- TODO: Найти больше примеров HTML плагинов -->

Узнать какие плагины используются в документе можно через аттрибут документа [`document.embeds`](https://html.spec.whatwg.org/multipage/dom.html#dom-document-embeds) и [`document.plugins`](https://html.spec.whatwg.org/multipage/dom.html#dom-document-plugins)
