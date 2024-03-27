# Origin

## Documentation
- [IETF RFC 6454 - The Web Origin Concept](https://datatracker.ietf.org/doc/html/rfc6454)
- [WHATWG - HTML Origins](https://html.spec.whatwg.org/multipage/browsers.html#origin)

## Articles
- [stackoverflow *comment* - When do browsers send the Origin header? When do browsers set the origin to null?](https://stackoverflow.com/a/42242802)

___

**Origin (источник/происхождение)** - концепцию происхождения (**origin**) определяют пользовательские агенты (**user agent**). Они группируют URI в домены защиты, называемые **origins**.

Предполагается, что два участника веб-платформы, имеющие общее происхождение  (**origin**), доверяют друг другу и обладают одинаковыми полномочиями. Участники с разным происхождением (**origin**) считаются потенциально враждебными по отношению друг к другу и изолированы друг от друга в разной степени.

Хотя пользовательские агенты (**user agent**) группируют URI в origins, не каждый ресурс в **origin** обладает одинаковыми полномочиями. Пользовательские агенты определяют, какие полномочия предоставлять ресурсу, изучая его тип носителя (**media type**).

В сущности пользовательские агенты (**user agent**) изолируют различные источники (**origins**) и обеспечивают контролируемую связь между источниками. Детали того, как пользовательские агенты (**user agent**) обеспечивают изоляцию и связь, различаются в зависимости от нескольких факторов, про которые можно причитать тут.

**Origin** обязательно состоит из следующих компонентов [URI синтаксиса](https://www.rfc-editor.org/rfc/rfc3986#section-3):
- [**`scheme`**](https://www.rfc-editor.org/rfc/rfc3986#section-3.1)
- [**`host`**](https://www.rfc-editor.org/rfc/rfc3986#section-3.2.2)
- [**`port`**](https://www.rfc-editor.org/rfc/rfc3986#section-3.2.3) || null, так как может быть скрыт после **[HTTP(S) нормализации](https://www.rfc-editor.org/rfc/rfc9110#section-4.2.3)**
- [`domain`](https://html.spec.whatwg.org/multipage/browsers.html#concept-origin-domain) || null - Значение можно только получать через аттрибут документа `document.domain`, но не назначать. Этот аттрибут [в будущем удалял из спецификации](https://html.spec.whatwg.org/multipage/browsers.html#dom-document-domain)

Два источника (**origin**) **ДОЛЖНЫ (MUST)** различаться, если они отличаются чем либо из `scheme`, `host` или `port`.

<!-- TODO: Разобраться и написать про opaque origin. https://stackoverflow.com/a/42242802 -->

#### Same origin

Два источника, являются одним и тем же источником (*same origin*), если [следующий алгоритм](https://html.spec.whatwg.org/multipage/browsers.html#same-origin) возвращает `true`.

Два источника, A и B, являются «одним и тем же исходным доменом» (*same origin-domain*), если [следующий алгоритм](https://html.spec.whatwg.org/multipage/browsers.html#same-origin-domain) возвращает `true`.

#### Same site

Два источника, A и B, являются одним и тем же сайтом (*same site*), если [следующий алгоритм](https://html.spec.whatwg.org/multipage/browsers.html#same-site) возвращает `true`.

Два источника, A и B, являются одним и тем же сайтом без схемы (*schemelessly same site*), если [следующий алгоритм](https://html.spec.whatwg.org/multipage/browsers.html#schemelessly-same-site) возвращает значение `true`.

В отличие от концепций "same origin" и "same origin-domain", для "schemelessly same site" и "same site" компоненты порта (`port`) и домена (`domain`) игнорируются.

По причинам, [объясненным в URL](https://url.spec.whatwg.org/#warning-avoid-psl), следует по возможности избегать концепции ["same site"](https://html.spec.whatwg.org/multipage/browsers.html#same-site) и ["schemelessly same site"](https://html.spec.whatwg.org/multipage/browsers.html#schemelessly-same-site) в пользу концепции [**same origin**](https://html.spec.whatwg.org/multipage/browsers.html#same-origin)

___

## Fields

### Origin - Источник 🎩➡️🕵️

**`Origin`** - это HTTP-заголовок, который отправляется автоматически браузерами при выполнении кросс-доменных запросов, и указывает источник, с которого пользовательский агент выполняет запрос. Этот источник определяется API, который инициировал запрос. Например, если **DOM API** инициирует загрузку скрипта, или **Fetch API** запускает запрос на другой ресурс, то заголовок `Origin` может быть включен в HTTP-запрос.

Заголовок `Origin` используется для обеспечения безопасности, позволяя серверам проверять, что кросс-доменные запросы исходят из доверенных источников. Если пользовательский агент должен запросить ресурсы, встроенные в страницу или полученные через скрипты, то источник этих запросов может быть указан в заголовке `Origin`.

___

Получить значение **origin** можно несколькими способами:
- [`window.location.origin`](https://html.spec.whatwg.org/multipage/nav-history-apis.html#dom-location-origin)
- [`window.origin`](https://html.spec.whatwg.org/multipage/webappapis.html#dom-origin-dev)
