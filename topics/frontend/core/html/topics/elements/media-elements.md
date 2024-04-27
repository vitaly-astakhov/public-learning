# [Media elements](https://html.spec.whatwg.org/multipage/media.html#media-elements)

## Overview

### [`<video>` element](https://html.spec.whatwg.org/multipage/media.html#the-video-element) 🏷️

Элемент **`<video>`** используется для воспроизведения видео или фильмов, а также аудиофайлов с субтитрами.

Элемент **`<video>`** представляет собой то, что задано для первого условия соответствия в приведенном ниже списке:

- [Когда видеоданные недоступны](https://html.spec.whatwg.org/multipage/media.html#the-video-element:dom-media-readystate)
  - Элемент **`<video>`** представляет постерный кадр ([*poster frame*](https://html.spec.whatwg.org/multipage/media.html#poster-frame)), если таковая имеется, или же прозрачно-черную, без естественных размеров.
- [Когда элемент **`<video>`** приостанавливается, текущей позицией воспроизведения является первый кадр видео, и для элемента устанавливается флажок показывать постер](https://html.spec.whatwg.org/multipage/media.html#the-video-element:dom-media-paused)
  - Элемент **`<video>`** представляет свой постерный кадр ([*poster frame*](https://html.spec.whatwg.org/multipage/media.html#poster-frame)), если таковой имеется, или первый кадр видео.
- [Когда элемент **`<video>`** приостановлен, а кадр видео, соответствующий текущей позиции воспроизведения, недоступен (например, из-за поиска или буферизации видео)](https://html.spec.whatwg.org/multipage/media.html#the-video-element:dom-media-paused-2)
- [Когда элемент **`<video>`** потенциально не воспроизводится и не приостанавливается (например, при поиске или остановке воспроизведения)](https://html.spec.whatwg.org/multipage/media.html#the-video-element:potentially-playing)
  - Элемент **`<video>`** представляет собой последний кадр видео, который был отрендерен.
- [Когда элемент **`<video>`** приостановлен](https://html.spec.whatwg.org/multipage/media.html#the-video-element:dom-media-paused-4)
  - Элемент **`<video>`** представляет кадр видео, соответствующий текущей позиции воспроизведения.
- [В противном случае (элемент **`<video>`** имеет видеоканал и потенциально воспроизводится)](https://html.spec.whatwg.org/multipage/media.html#the-video-element:potentially-playing-2)
  - Элемент **`<video>`** представляет кадр видео в непрерывно увеличивающейся "текущей" позиции. Когда текущее положение воспроизведения изменяется таким образом, что последний отрисованный кадр больше не является кадром, соответствующим текущему положению воспроизведения в видео, необходимо отрисовать новый кадр.

### [`<audio>` element](https://html.spec.whatwg.org/multipage/media.html#the-audio-element) 🏷️

Элемент **`<audio>`** представляет собой звук или аудиопоток.

### [`<track>` element](https://html.spec.whatwg.org/multipage/media.html#the-track-element) 🏷️

Элемент **`<track>`** позволяет авторам указывать явные внешние текстовые дорожки с таймером для мультимедийных элементов. Сам по себе он ничего не представляет.
