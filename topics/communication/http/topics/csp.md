# Content Security Policy (CSP)

## Materials

- [W3C - Content Security Policy Level 3](https://w3c.github.io/webappsec-csp/)
- [Content Security Policy (CSP) Quick Reference Guide](https://content-security-policy.com/)
- [Content Security Policy Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)

## Tools

- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)

## Table of contents

- [Overview](#overview)
- [Fields](#fields)
  - [Content-Security-Policy 🎩⬅️](#content-security-policy-️)
  - [Content-Security-Policy-Report-Only 🎩⬅️](#content-security-policy-report-only-️)
- [Content Security Policy Directives](#content-security-policy-directives)
  - [Fetch Directives](#fetch-directives)
    - [`child-src`](#child-src)
    - [`connect-src`](#connect-src)
    - [`default-src`](#default-src)
    - [`font-src`](#font-src)
    - [`frame-src`](#frame-src)
    - [`img-src`](#img-src)
    - [`manifest-src`](#manifest-src)
    - [`media-src`](#media-src)
    - [`object-src`](#object-src)
    - [`script-src`](#script-src)
      - [`script-src-elem`](#script-src-elem)
      - [`script-src-attr`](#script-src-attr)
    - [`style-src`](#style-src)
      - [`style-src-elem`](#style-src-elem)
      - [`style-src-attr`](#style-src-attr)
  - [Document Directives](#document-directives)
    - [`base-uri`](#base-uri)
    - [`sandbox`](#sandbox)
  - [Navigation Directives](#navigation-directives)
    - [`form-action`](#form-action)
    - [`frame-ancestors`](#frame-ancestors)
  - [Reporting Directives](#reporting-directives)
    - [`report-uri` (deprecated)](#report-uri-deprecated)
    - [`report-to`](#report-to)
  - [Other Directives](#other-directives)
    - [`webrtc`](#webrtc)
    - [`worker-src`](#worker-src)
- [HTML and API's](#html-and-apis)
  - [CSP within `<meta>` element](#csp-within-meta-element)

## Overview

Политика безопасности контента (*Content Security Policy*) - это инструмент, который разработчики могут использовать для блокировки своих приложений различными способами, снижая риск уязвимостей, связанных с внедрением контента, таких как межсайтовый скриптинг, и снижая привилегии, с которыми выполняются их приложения.

CSP не предназначен в качестве первой линии защиты от уязвимостей, связанных с внедрением контента. Вместо этого CSP лучше всего использовать в качестве комплексной защиты. Это уменьшает вред, который может нанести вредоносное внедрение, но не заменяет тщательную проверку ввода и кодирование вывода.

Политика (*policy*) определяет разрешенное (*allowed*) и ограниченное (*restricted*) поведение и может быть применена к [`Document`](https://dom.spec.whatwg.org/#document), [`WorkerGlobalScope`](https://html.spec.whatwg.org/multipage/workers.html#workerglobalscope), или [`WorkletGlobalScope`](https://html.spec.whatwg.org/multipage/worklets.html#workletglobalscope).

Каждая политика (*policy*) имеет:

- [**directive set**](https://w3c.github.io/webappsec-csp/#policy-directive-set) (*набор директив*), который представляет собой упорядоченный набор директив ([`directives`](https://w3c.github.io/webappsec-csp/#directives)), определяющих применения политики.
- [**disposition**](https://w3c.github.io/webappsec-csp/#policy-disposition) (*расположение*) - "enforce" или "report".
- [**source**](https://w3c.github.io/webappsec-csp/#policy-source) (*источник*) - "header" или "meta".
- [**self-origin**](https://w3c.github.io/webappsec-csp/#policy-self-origin) (*самостоятельное происхождение*) - используется при сопоставлении ключевого слова ['self'](https://w3c.github.io/webappsec-csp/#grammardef-self).

Сервер **МОЖЕТ (MAY)** объявить политику для конкретного представления ресурса ([*resource representation*](https://tools.ietf.org/html/rfc9110#section-3.2)) с помощью поля заголовка HTTP-ответа, значением которого является сериализованный CSP ([*serialized CSP*](https://w3c.github.io/webappsec-csp/#serialized-csp)).

Политика также может быть объявлена встроенной в HTML-документ с помощью атрибута [`http-equiv`](https://html.spec.whatwg.org/multipage/semantics.html#attr-meta-http-equiv) HTML элемента [`<meta>`](https://html.spec.whatwg.org/multipage/semantics.html#meta)

## Fields

Сервер **МОЖЕТ (MAY)** отправлять разные значения полей заголовков **`Content-Security-Policy`** и **`Content-Security-Policy-Report-Only`** с разными представлениями ([*representations*](https://tools.ietf.org/html/rfc9110#section-3.2)) одного и того же ресурса.

Когда пользовательский агент (*user agent*) получает полей заголовков **`Content-Security-Policy`** и **`Content-Security-Policy-Report-Only`** он **ДОЛЖЕН (MUST)** проанализировать ([*parse*](https://w3c.github.io/webappsec-csp/#abstract-opdef-parse-a-serialized-csp)) и применить ([*enforce*](https://w3c.github.io/webappsec-csp/#enforced)) каждый сериализованный CSP ([*serialized CSP*](https://w3c.github.io/webappsec-csp/#serialized-csp)), который в нем содержится.

### [Content-Security-Policy](https://w3c.github.io/webappsec-csp/#csp-header) 🎩⬅️

**`Content-Security-Policy`** -  это HTTP-заголовок, который отправляется сервером и является предпочтительным механизмом передачи политики с сервера клиенту.

### [Content-Security-Policy-Report-Only](https://w3c.github.io/webappsec-csp/#cspro-header) 🎩⬅️

**`Content-Security-Policy-Report-Only`** -  это HTTP-заголовок, который отправляется сервером и позволяет веб-разработчикам экспериментировать с политиками, отслеживая (но не применяя) их действие.

Это поле заголовка позволяет разработчикам последовательно составлять свою политику безопасности, внедряя политику только для отчетов на основе наилучшей оценки поведения своего сайта, отслеживая сообщения о нарушениях, а затем переходя к принудительной политике, как только они обретут уверенность в таком поведении.

## [Content Security Policy Directives](https://w3c.github.io/webappsec-csp/#csp-directives)

Каждая политика (*policy*) содержит упорядоченный набор директив, каждая из которых управляет определенным поведением.

Каждая директива представляет собой пару имя / значение ([name](https://w3c.github.io/webappsec-csp/#directive-name) / [value](https://w3c.github.io/webappsec-csp/#directive-value))

Сериализованная директива - это строка, состоящая из одного или нескольких токенов, разделенных [обязательными пробелами](https://w3c.github.io/webappsec-csp/#grammardef-required-ascii-whitespace).

<!-- Может добавить информацию об алгоритмах, с которым ассоциируются директивы, например [pre-request check](https://w3c.github.io/webappsec-csp/#directive-pre-request-check) -->

Значения (*value*) многих директив состоят из списков источников ([*source lists*](https://w3c.github.io/webappsec-csp/#source-lists)): наборов строк, которые идентифицируют содержимое, которое может быть извлечено и потенциально внедрено или выполнено. Каждая строка представляет один из следующих типов исходных выражений ([source expression](https://w3c.github.io/webappsec-csp/#source-expression)):

- `'none'`
- `*` aka wildcard
- [**keyword-source**](https://w3c.github.io/webappsec-csp/#grammardef-keyword-source)
  - `'self'`
  - `'unsafe-inline'`
  - `'unsafe-eval'`
  - [`'strict-dynamic'`](https://w3c.github.io/webappsec-csp/#strict-dynamic-usage)
  - [`'unsafe-hashes'`](https://w3c.github.io/webappsec-csp/#unsafe-hashes-usage)
  - `'report-sample'`
  - `'unsafe-allow-redirects'`
  - `'wasm-unsafe-eval'`
- [**scheme-source**](https://w3c.github.io/webappsec-csp/#grammardef-scheme-source) - указывает источник, который соответствуют любому ресурсу, имеющему указанную схему. Например, "https:" / "custom-scheme:" / "another.custom-scheme:"
- [**host-source**](https://w3c.github.io/webappsec-csp/#grammardef-host-source) - например, "example.com" / "*.example.com" / "https://*.example.com:12/path/to/file.js"
- [**nonce-source**](https://w3c.github.io/webappsec-csp/#grammardef-nonce-source) - например, nonce-[nonce goes here]. Одноразовые значения (*nonces*) переопределяют другие ограничения, присутствующие в директиве, в которой они предоставляются. Если сервер предоставляет выражение из одноразового источника ([*nonce-source*](https://w3c.github.io/webappsec-csp/#grammardef-nonce-source)) как часть политики, сервер **ДОЛЖЕН (MUST)** генерировать уникальное значение каждый раз, когда он передает политику. Подробнее[^1][^2][^3].
- [**hash-source**](https://w3c.github.io/webappsec-csp/#grammardef-hash-source) aka digests - например,'sha256-[digest goes here]'

<!-- Разобраться почему это называется digests -->

### [Fetch Directives](https://w3c.github.io/webappsec-csp/#directives-fetch)

Директивы Fetch ([*Fetch directives*](https://w3c.github.io/webappsec-csp/#fetch-directives)) управляют локациями, из которых могут быть загружены определенные типы ресурсов.

#### [`child-src`](https://w3c.github.io/webappsec-csp/#directive-child-src)

Директива **`child-src`** управляет созданием дочерних элементов навигации ([*child navigables*](https://html.spec.whatwg.org/multipage/document-sequences.html#child-navigable)) (например, [`<iframe>`](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#the-iframe-element) и [`<frame>`](https://html.spec.whatwg.org/multipage/obsolete.html#frame) навигации) и контекстами выполнения Worker (*Worker execution contexts*).

The `child-src` directive governs the creation of [child navigables](https://html.spec.whatwg.org/multipage/document-sequences.html#child-navigable) (e.g. [`<iframe>`](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#the-iframe-element) and [`<frame>`](https://html.spec.whatwg.org/multipage/obsolete.html#frame) navigations) and Worker execution contexts.

#### [`connect-src`](https://w3c.github.io/webappsec-csp/#directive-connect-src)

Директива **`connect-src`** ограничивает URL-адреса, которые могут быть загружены используя интерфейсы сценариев (*script interfaces*), которые напрямую подключаются (*connect*) к внешнему серверу для отправки (*send*) или получения (*receive*) информации.

Директива **`connect-src`** управляет запросами, которые передают или получают данные из других источников. Сюда входят такие API, как [`fetch()`](https://fetch.spec.whatwg.org/#dom-global-fetch), [`XMLHttpRequest`](https://xhr.spec.whatwg.org/#xmlhttprequest), [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#eventsource), [`navigator.sendBeacon()`](https://www.w3.org/TR/beacon/#dom-navigator-sendbeacon) и аттрибут [`ping`](https://html.spec.whatwg.org/multipage/links.html#ping) элемента [`<a>`](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-a-element).

Директива **`connect-src`** также управляет подключениями [`WebSocket`](https://websockets.spec.whatwg.org/#websocket), хотя технически они не являются частью Fetch.

#### [`default-src`](https://w3c.github.io/webappsec-csp/#directive-default-src)

Директива **`default-src`** служит запасным вариантом (*fallback*) для других fetch директив ([*fetch directives*](https://w3c.github.io/webappsec-csp/#fetch-directives)).

Если в политике присутствует директива **`default-src`**, ее значение будет использоваться в качестве списка источников политики по умолчанию. То есть, когда задано значение **`default-src`**, каждая fetch директива, которая не задана явно (*explicitly*), будет возвращена к значению (*fall back*), указанному в **`default-src`**.

#### [`font-src`](https://w3c.github.io/webappsec-csp/#directive-font-src)

Директива **`font-src`** ограничивает URL-адреса, с которых могут быть загружены ресурсы шрифтов.

#### [`frame-src`](https://w3c.github.io/webappsec-csp/#directive-frame-src)

Директива **`frame-src`** ограничивает URL-адреса, которые могут быть загружены в дочерние навигационные элементы

#### [`img-src`](https://w3c.github.io/webappsec-csp/#directive-img-src)

Директива **`img-src`** ограничивает URL-адреса, с которых могут быть загружены ресурсы изображений.

#### [`manifest-src`](https://w3c.github.io/webappsec-csp/#directive-manifest-src)

Директива **`manifest-src`** ограничивает URL-адреса, с которых могут быть загружены [манифесты приложений](https://www.w3.org/TR/appmanifest/).

#### [`media-src`](https://w3c.github.io/webappsec-csp/#directive-media-src)

Директива **`media-src`** ограничивает URL-адреса, с которых могут загружаться ресурсы видео, аудио и связанных с ними текстовых дорожек.

#### [`object-src`](https://w3c.github.io/webappsec-csp/#directive-object-src)

Директива **`object-src`** ограничивает URL-адреса, с которых может быть загружен контент плагина.

#### [`script-src`](https://w3c.github.io/webappsec-csp/#directive-script-src)

Директива **`script-src`** ограничивает локации, из которых могут выполняться сценарии.

Директива  **`script-src`** действует как резервный вариант по умолчанию для всех адресатов, подобных сценарию (включая адресаты, относящиеся к конкретному работнику, если worker-src отсутствует). Если не требуется детализация, следует использовать  **`script-src`** вместо `script-src-attr` и `script-src-elem`, поскольку в большинстве ситуаций нет особой причины иметь отдельные списки разрешений для встроенных обработчиков событий (*event handlers*) и элементов [`<script>`](https://html.spec.whatwg.org/multipage/scripting.html#script).

##### [`script-src-elem`](https://w3c.github.io/webappsec-csp/#directive-script-src-elem)

Директива **`script-src-elem`** применяется ко всем запросам скрипта и блокам скрипта. Иными словами, применяется только к тегам и блокам скриптов (`<script>`), не применяется к встроенным обработчикам событий, таким как onclick

##### [`script-src-attr`](https://w3c.github.io/webappsec-csp/#directive-script-src-attr)

Директива **`script-src-attr`** применяется к обработчикам событий (*event handlers*) и, если она присутствует, переопределяет директиву `script-src` для соответствующих проверок. Иными словами, применяется только к атрибутам отвечающим, за обработку события (*event handlers*) таким как `onclick`, `onmouseover` и т.д.

#### [`style-src`](https://w3c.github.io/webappsec-csp/#directive-style-src)

Директива **`style-src`** ограничивает локации, из которых стили могут быть применены к документу ([*Document*](https://dom.spec.whatwg.org/#document)).

##### [`style-src-elem`](https://w3c.github.io/webappsec-csp/#directive-style-src-elem)

Директива `style-src-elem` определяет поведение стилей, за исключением стилей, определенных во встроенных атрибутах.

##### [`style-src-attr`](https://w3c.github.io/webappsec-csp/#directive-style-src-attr)

Директива **`style-src-attr`** определяет поведение атрибутов стиля. Иными словами, применяется только к атрибутам отвечающим за применение стилей, т.е. `style`

### [Document Directives](https://w3c.github.io/webappsec-csp/#directives-document)

#### [`base-uri`](https://w3c.github.io/webappsec-csp/#directive-base-uri)

Директива **`base-uri`** ограничивает URL-адреса, которые могут использоваться в элементе [`<base>`](https://html.spec.whatwg.org/multipage/semantics.html#the-base-element) документа

#### [`sandbox`](https://w3c.github.io/webappsec-csp/#directive-sandbox)

Директива **`sandbox`** определяет политику HTML-изолированной среды, которую пользовательский агент будет применять к ресурсу, точно так же, как если бы он был включен в [`<iframe>`](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#the-iframe-element) со свойством [sandbox](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#attr-iframe-sandbox).

Директива **`sandbox`** не содержит требований к отчетности (*no reporting requirements*); она будет полностью проигнорирована, если будет представлена в заголовке [`Content-Security-Policy-Report-Only`](https://w3c.github.io/webappsec-csp/#header-content-security-policy-report-only) или в HTML элементе [`<meta>`](https://html.spec.whatwg.org/multipage/semantics.html#meta).

### [Navigation Directives](https://w3c.github.io/webappsec-csp/#directives-navigation)

#### [`form-action`](https://w3c.github.io/webappsec-csp/#directive-form-action)

Директива **`form-action`** ограничивает URL-адреса, которые могут использоваться в качестве цели для отправки формы из данного контекста.

#### [`frame-ancestors`](https://w3c.github.io/webappsec-csp/#directive-frame-ancestors)

### [Reporting Directives](https://w3c.github.io/webappsec-csp/#directives-reporting)

#### [`report-uri`](https://w3c.github.io/webappsec-csp/#directive-report-uri) (deprecated)

#### [`report-to`](<https://w3c.github.io/webappsec-csp/#directive-report-to>)

Директива **`report-to`** определяет конечную точку отчетности ([*reporting endpoint*](https://www.w3.org/TR/reporting-1/#endpoint)), в которую должны направляться сообщения о нарушениях (*violation*).

### [Other Directives](https://w3c.github.io/webappsec-csp/#directives-other)

#### [`webrtc`](https://w3c.github.io/webappsec-csp/#directive-webrtc)

Директива **`webrtc`** ограничивает возможность установления соединений через [WebRTC](https://w3c.github.io/webrtc-pc/).

#### [`worker-src`](https://w3c.github.io/webappsec-csp/#directive-worker-src)

Директива **`worker-src`** ограничивает URL-адреса, которые могут быть загружены как [`Worker`](https://html.spec.whatwg.org/multipage/workers.html#worker), [`SharedWorker`](https://html.spec.whatwg.org/multipage/workers.html#sharedworker), или [`ServiceWorker`](https://www.w3.org/TR/service-workers/#serviceworker).

## HTML and API's

### [CSP within `<meta>` element](https://w3c.github.io/webappsec-csp/#meta-element)

Документ может предоставлять политику с помощью одного или нескольких HTML элементов [**`<meta>`**](https://html.spec.whatwg.org/multipage/semantics.html#meta), атрибуты http-equiv которых соответствуют строке "Content-Security-Policy" без учета регистра в ASCII

> [!NOTE]
> **`Content-Security-Policy-Report-Only`** поле не поддерживается внутри элемента [**`<meta>`**](https://html.spec.whatwg.org/multipage/semantics.html#meta).
>
> Также не используются директивы report-uri, frame-ancestors и sandbox.

[^1]: [Nonce Reuse](https://w3c.github.io/webappsec-csp/#security-nonces)
[^2]: [Nonce Hijacking](https://w3c.github.io/webappsec-csp/#security-nonce-hijacking)
[^3]: [Nonce Retargeting](https://w3c.github.io/webappsec-csp/#security-nonce-retargeting)
