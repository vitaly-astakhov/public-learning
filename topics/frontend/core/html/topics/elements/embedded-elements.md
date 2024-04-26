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

У элемента **`<img>`** есть две похожих группы свойств аттрибутов DOM интерфейса: [`width`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-width)/[`height`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-height) и [`naturalWidth`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-naturalwidth)/[`naturalHeight`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-naturalheight).

DOM атрибуты [`width`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-width) и [`height`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-height) должны возвращать отображаемую ширину и высоту изображения в пикселях CSS ([*CSS pixels*](https://drafts.csswg.org/css-values/#px)), если изображение отрендерино ([*being rendered*](https://html.spec.whatwg.org/multipage/rendering.html#being-rendered)); или же естественную ширину и высоту изображения с поправкой на плотность ([*density-corrected natural width and height*](https://html.spec.whatwg.org/multipage/images.html#density-corrected-intrinsic-width-and-height)) в пикселях CSS, если изображение имеет естественную ширину и высоту с поправкой на плотность ([*density-corrected natural width and height*](https://html.spec.whatwg.org/multipage/images.html#density-corrected-intrinsic-width-and-height)) и доступно ([`available`](https://html.spec.whatwg.org/multipage/images.html#img-available)) но не отрендерино ([*being rendered*](https://html.spec.whatwg.org/multipage/rendering.html#being-rendered)); или же `0`, если изображение недоступно или не имеет естественных ширины и высоты с поправкой на плотность.

DOM атрибуты [`naturalWidth`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-naturalwidth) и [`naturalHeight`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-naturalheight) должны возвращать естественные ширину и высоту изображения с поправкой на плотность ([*density-corrected natural width and height*](https://html.spec.whatwg.org/multipage/images.html#density-corrected-intrinsic-width-and-height)) в пикселях CSS, если изображение имеет естественные ширину и высоту с поправкой на плотность ([*density-corrected natural width and height*](https://html.spec.whatwg.org/multipage/images.html#density-corrected-intrinsic-width-and-height)) и доступно ([`available`](https://html.spec.whatwg.org/multipage/images.html#img-available)), или же `0`. [CSS]

> [!NOTE]
> При добавлении картинки, которая была создана через `new Image()`, рекомендуется вместо обработчиков событий `onload` и `onerror` использовать асинхронный метод [`decode()`](https://html.spec.whatwg.org/multipage/embedded-content.html#dom-img-decode).
>
> Так, например, сделано в [`next/image`](https://github.com/vercel/next.js/blob/433faa8436a2f1db9fc02d67867f5e08c8cf433b/packages/next/src/client/image-component.tsx#L75)
>
> Еще примеры: [Пример 1](https://github.com/tamagui/tamagui/blob/b20fa8fae92a3410a47e6569928a409ecdc6a9b5/packages/react-native-web-internals/src/modules/ImageLoader/index.tsx#L132), [Пример 2](https://github.com/outline/outline/blob/bf848f3a2f7d7577b7e33a2b6b15580a331320b6/shared/editor/components/ImageZoom/Controlled.tsx#L390)
> ___
> [Источник](https://html.spec.whatwg.org/multipage/embedded-content.html#:~:text=Without%20the%20decode)

## [Media elements](https://html.spec.whatwg.org/multipage/media.html#media-elements)

### [`video` element](https://html.spec.whatwg.org/multipage/media.html#the-video-element)

### [`audio` element](https://html.spec.whatwg.org/multipage/media.html#the-audio-element)

### [`track` element](https://html.spec.whatwg.org/multipage/media.html#the-track-element)
