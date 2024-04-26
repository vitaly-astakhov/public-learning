# Images

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

Получить все картинки, которые находятся доступны в HTML документе можно через аттрибут `document.images`.

#### [Alternative text](https://html.spec.whatwg.org/multipage/images.html#alt)

Аттрибут `alt` означает альтернативный для картинки текст.

Области пользы альтернативного текста:

- не загруженная картинка
- программа для чтения с экрана (*screen readers*)

Обычно атрибут `alt` необходимо указать, и его значение не должно быть пустым; это значение должно быть подходящей заменой изображению.

Наиболее общее правило, которое следует учитывать при написании альтернативного текста, заключается в следующем: цель состоит в том, чтобы замена каждого изображения текстом с его атрибутом `alt` не меняла смысла страницы.

Значение атрибута `alt` никогда не должно содержать текст, который можно было бы считать подписью (*caption*) к изображению, заголовком (*title*) или легендой (*legend*). Предполагается, что он должен содержать заменяющий текст, который пользователи могли бы использовать вместо изображения; он не предназначен для дополнения изображения. Атрибут `[title](https://html.spec.whatwg.org/multipage/dom.html#attr-title)` может быть использован для получения дополнительной информации.

Так же значение атрибута `alt` не должно повторять информацию, которая уже указана в тексте рядом с изображением.

> [!NOTE]
> Один из способов придумать альтернативный текст - это представить, как бы вы читали страницу с изображением кому-нибудь по телефону, не упоминая о том, что там присутствует изображение. Что бы вы ни сказали вместо изображения, это, как правило, хорошее начало для написания альтернативного текста.

Подробнее про написание альтернативного текст можно прочитать в тут: [Requirements for providing text to act as an alternative for images](https://html.spec.whatwg.org/multipage/images.html#alt)

#### Declarative `<img>` responsiveness

#### [Device-pixel-ratio-based selection when the rendered size of the image is fixed](introduction-3:device-pixel-ratio-2)

Атрибуты [`src`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-src) и [`srcset`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset) элемента **`<img>`** можно использовать, используя дескриптор плотности пикселей ([*pixel density descriptor*](https://html.spec.whatwg.org/multipage/images.html#pixel-density-descriptor)), т.е. *`x`*, для получения нескольких изображений, различающихся только по размеру (изображение меньшего размера является уменьшенной версией изображения большего размера).

Пользовательский агент может выбрать любой из предоставленных ресурсов в зависимости от плотности пикселей экрана пользователя (*pixel density*), уровня масштабирования (*zoom level*) и, возможно, других факторов, таких как условия работы сети пользователя.

Для обеспечения обратной совместимости со старыми пользовательскими агентами, которые еще не понимают атрибут [`srcset`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset), один из URL-адресов указан в атрибуте `src` элемента **`<img>`**. В результате даже в старых пользовательских агентах будет отображаться что-то полезное (хотя, возможно, с более низким разрешением, чем хотелось бы пользователю). Для новых пользовательских агентов атрибут `src` участвует в выборе ресурса, как если бы он был указан в [`srcset`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset) с помощью дескриптора *`1x`*.

```html
<img src="/uploads/100-marie-lloyd.jpg"
     srcset="/uploads/150-marie-lloyd.jpg 1.5x, /uploads/200-marie-lloyd.jpg 2x"
     alt="" width="100" height="150">
```

> [!NOTE]
> Дескриптор *`x`* не подходит, когда размер отображаемого изображения зависит от ширины видового экрана ([*viewport-based selection*](https://html.spec.whatwg.org/multipage/images.html#viewport-based-selection)), но может использоваться вместе с [art direction](https://html.spec.whatwg.org/multipage/images.html#art-direction).

[Примеры device-pixel-ratio-based selection 📂](./examples/example-img-responsiveness.md#device-pixel-ratio-based-selection)

#### [Viewport-based selection](https://html.spec.whatwg.org/multipage/images.html#introduction-3:viewport-based-selection-2)

Атрибуты [`srcset`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset) и [`sizes`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-sizes), используя дескриптор ширины ([*width descriptor*](https://html.spec.whatwg.org/multipage/images.html#width-descriptor)), т.е. *`w`*, можно использовать для получения нескольких изображений, различающихся только по размеру (изображение меньшего размера является уменьшенной версией изображения большего размера).

Пользовательский агент рассчитает эффективную плотность пикселей для каждого изображения на основе указанных дескрипторов w и указанного размера визуализируемого изображения в атрибуте [`sizes`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-sizes). Затем он может выбрать любой из заданных ресурсов в зависимости от плотности пикселей экрана пользователя (*pixel density*), уровня масштабирования (*zoom level*) и, возможно, других факторов, таких как условия работы сети пользователя.

```html
<img sizes="100vw" srcset="wolf-400.jpg 400w, wolf-800.jpg 800w, wolf-1600.jpg 1600w"
     src="wolf-400.jpg" alt="The rad wolf">

<img sizes="(max-width: 30em) 100vw, (max-width: 50em) 50vw, calc(33vw - 100px)"
srcset="swing-200.jpg 200w, swing-400.jpg 400w, swing-800.jpg 800w, swing-1600.jpg 1600w"
src="swing-400.jpg" alt="Kettlebell Swing">

<img loading="lazy" width="200" height="200"
     sizes="auto, (max-width: 30em) 100vw, (max-width: 50em) 50vw, calc(33vw - 100px)"
     srcset="swing-200.jpg 200w, swing-400.jpg 400w, swing-800.jpg 800w, swing-1600.jpg 1600w"
     src="swing-400.jpg" alt="Kettlebell Swing">
```

#### [Art direction-based selection](https://html.spec.whatwg.org/multipage/images.html#introduction-3:art-direction-3)

Элемент [`<picture>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) и элемент [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element) вместе с атрибутом [`media`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-source-media) могут использоваться для создания нескольких изображений, различающихся по содержанию (например, изображение меньшего размера может быть обрезанной версией изображения большего размера).

```html
<picture>
  <source media="(min-width: 45em)" srcset="large.jpg">
  <source media="(min-width: 32em)" srcset="med.jpg">
  <img src="small.jpg" alt="The wolf runs through the snow.">
</picture>
```

Пользовательский агент выберет первый элемент [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element), которому соответствует медиазапрос (*media query*) в атрибуте [`media`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-source-media), а затем выберет соответствующий URL-адрес из его атрибута [srcset](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-source-srcset).

Размер отображаемого изображения зависит от выбранного ресурса. Чтобы указать размеры, которые пользовательский агент может использовать перед загрузкой изображения, можно использовать CSS.

```css
img { width: 300px; height: 300px }
@media (min-width: 32em) { img { width: 500px; height:300px } }
@media (min-width: 45em) { img { width: 700px; height:400px } }
```

#### [Image format-based selection](https://html.spec.whatwg.org/multipage/images.html#introduction-3:image-format-based-selection)

Атрибут [`type`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-source-type) в элементе [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element) может использоваться для предоставления нескольких изображений в разных форматах.

```html
<picture>
 <source srcset="/uploads/100-marie-lloyd.webp" type="image/webp">
 <source srcset="/uploads/100-marie-lloyd.jxr" type="image/vnd.ms-photo">
 <img src="/uploads/100-marie-lloyd.jpg" alt="" width="100" height="150">
</picture>

```

В этом примере пользовательский агент выберет первый источник, который имеет атрибут  [`type`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-source-type) с поддерживаемым типом MIME. Если пользовательский агент поддерживает WebP-изображения, будет выбран первый элемент [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element). Если нет, но пользовательский агент поддерживает изображения в формате JPEG XR, будет выбран второй элемент [`<source>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-source-element). Если ни один из этих форматов не поддерживается, будет выбран элемент [`<img>`](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element) .

#### [Processing model](https://html.spec.whatwg.org/multipage/images.html#images-processing-model)

Элемент `<img>` содержит текущий запрос (*current request*) и ожидающий выполнения запрос (*pending request*). Текущему запросу изначально присваивается значение нового запроса на изображение (*image request*). Ожидающему запросу изначально присваивается значение `null`.

Запрос на изображение ([*image request*](https://html.spec.whatwg.org/multipage/images.html#image-request)) содержит:

- [**state**](https://html.spec.whatwg.org/multipage/images.html#img-req-state) - состояние запроса изображения может быть одним из следующих
  - **unavailable** (default) - Пользовательский агент не получил никаких данных об изображении или получил часть или все данные об изображении, но еще не декодировал достаточную часть изображения, чтобы получить размеры изображения.
  - **partially available** - Пользовательский агент получил некоторые данные об изображении, и доступны, по крайней мере, размеры изображения.
  - **completely available** - Пользовательский агент получил все данные об изображении, и доступны, по крайней мере, размеры изображения.
  - **broken** - Пользовательский агент получил все данные изображения, какие только мог, но он не может даже расшифровать изображение в достаточной степени, чтобы получить размеры изображения (например, изображение повреждено, или формат не поддерживается, или данные не могут быть получены).
- [**current URL**](https://html.spec.whatwg.org/multipage/images.html#img-req-url) - это изначально пустая строкой.
- [**image data**](https://html.spec.whatwg.org/multipage/images.html#img-req-data) - это декодированные графические данные, полученные в ходе запроса на изображение.

Когда состояние запроса на изображение либо частично доступно (*partially available*), либо полностью доступно (*completely available*), считается, что запрос на изображение доступен ([*available*](https://html.spec.whatwg.org/multipage/images.html#img-available)).

##### Decoding images

Графические данные (*image data*) обычно кодируются (*encoded*) для уменьшения размера файла. Это означает, что для того, чтобы пользовательский агент мог отобразить изображение на экране, данные должны быть декодированы (*decoded*). Декодирование ([*decoding*](https://html.spec.whatwg.org/multipage/images.html#img-decoding-process)) - это процесс, который преобразует мультимедийные данные изображения в растровую форму, пригодную для отображения на экране. Обратите внимание, что этот процесс может быть медленным по сравнению с другими процессами, связанными с представлением контента. Таким образом, пользовательский агент может выбирать, когда выполнять декодирование, чтобы создать наилучший пользовательский опыт.

Указать один из следующих типов декодирования изображения можно через аттрибут [`decoding`](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-decoding):

- **sync** - Указывает на предпочтение синхронного декодирования этого изображения для атомарного представления с другим содержимым, т.е. синхронное декодирование изображения предотвращает представление другого контента до его завершения.
- **async** - Асинхронный указывает на предпочтение асинхронного декодирования этого изображения, чтобы избежать задержки представления другого содержимого, т.е. асинхронное декодирование изображения не препятствует отображению другого контента. Это позволяет быстрее отображать контент, не связанный с изображением. Однако содержимое изображения будет отсутствовать на экране до завершения декодирования.
- **auto** (default) - Указывает на отсутствие предпочтений в режиме декодирования (по умолчанию).
