# [Embedded content elements](https://html.spec.whatwg.org/multipage/embedded-content.html#embedded-content)

### [`<picture>` element](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element)

Элемент **`<picture>`** - это контейнер, который предоставляет несколько источников для содержащегося в нем элемента `<img>`, позволяя авторам декларативно управлять или давать подсказки пользовательскому агенту о том, какой графический ресурс использовать, исходя из плотности пикселей экрана, размера области просмотра, формата изображения и других факторов.

> [!NOTE]
> Элемент **`<picture>`** отличается от аналогичных элементов [`<video>`](https://html.spec.whatwg.org/multipage/media.html#the-video-element) и [`<audio>`](https://html.spec.whatwg.org/multipage/media.html#the-audio-element). Хотя все они содержат элементы [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element), атрибут `src` элемента [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element) не имеет значения, если элемент вложен в элемент **`<picture>`**, а алгоритм выбора ресурсов отличается. Кроме того, сам элемент **`<picture>`** ничего не отображает; он просто предоставляет контекст для содержащегося в нем элемента img, который позволяет ему выбирать из нескольких URL-адресов.

> [!NOTE]
> Элемент **`<picture>`** отличается от аналогичных элементов [`<video>`](https://html.spec.whatwg.org/multipage/media.html#the-video-element) и [`<audio>`](https://html.spec.whatwg.org/multipage/media.html#the-audio-element). Хотя все они содержат элементы [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element), некоторые аттрибуты элемента [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element) будут отличаться или не использоваться совсем, если элемент вложен в элемент **`<picture>`**. В частностью аттрибут `src` будет не имеет значения, а алгоритм выбора ресурсов отличается.
>
> Кроме того, сам элемент **`<picture>`** ничего не отображает; он просто предоставляет контекст для содержащегося в нем элемента `<img>`, который позволяет ему выбирать из нескольких URL-адресов.

### [`<source>` element](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element) 🏷️

Элемент **`<source>`** позволяет авторам указывать несколько альтернативных наборов источников (***sources***) для элементов `<img>` или несколько альтернативных медиаресурсов ([`media resources`](https://html.spec.whatwg.org/multipage/media.html#media-resource)) для медиаэлементов ([*media elements*](https://html.spec.whatwg.org/multipage/media.html#media-element)), таких как `<video>` и `<audio>`.

### [`<img>` element](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element) 🏷️

Элемент **`<img>`** представляет собой изображение (***image***).

[Подробнее про элемент **`<img>`** 📂](./images.md)

## [Media elements](https://html.spec.whatwg.org/multipage/media.html#media-elements)

### [`video` element](https://html.spec.whatwg.org/multipage/media.html#the-video-element)

### [`audio` element](https://html.spec.whatwg.org/multipage/media.html#the-audio-element)

### [`track` element](https://html.spec.whatwg.org/multipage/media.html#the-track-element)
