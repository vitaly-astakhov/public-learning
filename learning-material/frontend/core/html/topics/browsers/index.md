### [Policy containers](https://html.spec.whatwg.org/multipage/browsers.html#policy-containers)

Контейнер политик (**policy container**) — это структура, содержащая политики, которые применяются к [`Document` 📂](../document.md), [WorkerGlobalScope](https://html.spec.whatwg.org/multipage/workers.html#workerglobalscope) или [WorkletGlobalScope](https://html.spec.whatwg.org/multipage/worklets.html#workletglobalscope). Эта структура имеет следующие элементы:
- [CSP list](https://w3c.github.io/webappsec-csp/#csp-list)
- [embedder policy](https://html.spec.whatwg.org/multipage/browsers.html#embedder-policy)
- [referrer policy](https://w3c.github.io/webappsec-referrer-policy/#referrer-policy) - [referrer 📂](../../../../../communication/http/topics/referrer.md)
- [cross-origin opener policy](https://html.spec.whatwg.org/multipage/browsers.html#cross-origin-opener-policy)


## Opener

### Materials
- [Cross-origin opener policies - [HTML Spec]](https://html.spec.whatwg.org/multipage/browsers.html#cross-origin-opener-policies)
- [Cross-Origin-Opener-Policy response header (also known as COOP) - [gist.github]](https://gist.github.com/annevk/6f2dd8c79c77123f39797f6bdac43f3e)
- [Feature: Cross-Origin-Opener-Policy - [chromestatus]](https://chromestatus.com/feature/5432089535053824)

___

**Opener** - это концепция, отражающая идею родительского происхождения нового окна в веб-браузере. Эта модель реализована через свойство `opener` объекта `Window`, которое служит связующим звеном между исходным и новым окном, позволяя им обмениваться информацией и взаимодействовать друг с другом.

Передачу этого аттрибута контролирует политика [**cross-origin opener policy**](https://html.spec.whatwg.org/multipage/browsers.html#cross-origin-opener-policy) и некоторые типы ссылок (например, <а/>), через значения аттрибута `rel`: [`noopener`](https://html.spec.whatwg.org/multipage/links.html#link-type-noopener), [`opener`](https://html.spec.whatwg.org/multipage/links.html#link-type-opener)

### [Cross-Origin-Opener-Policy](https://html.spec.whatwg.org/multipage/browsers.html#cross-origin-opener-policies) 🎩⬅️
