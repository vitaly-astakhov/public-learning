# Permissions Policy

## Materials

### Documentation

- [Permissions Policy](https://w3c.github.io/webappsec-permissions-policy)
- [Permissions Policy Explainer](https://github.com/w3c/webappsec-permissions-policy/blob/main/permissions-policy-explainer.md)
- [Policy Controlled Features](https://github.com/w3c/webappsec-permissions-policy/blob/main/features.md)

## Table of contents

- [Overview](#overview)
  - [Policy-controlled Features](#policy-controlled-features)
  - [Allowlist](#allowlist)
- [Header fields](#header-fields)
  - [`Permissions-Policy` 🎩⬅️](#permissions-policy-️)
  - [`Permissions-Policy-Report-Only` 🎩⬅️](#permissions-policy-report-only-️)
- [HTML and API's](#html-and-apis)
  - [allow attribute](#allow-attribute)
  - [interface PermissionsPolicy](#interface-permissionspolicy)
- [Permissions API 📂](../../../../frontend/core/html/topics/permissions/readme.md)

## Overview

Политика разрешений (*Permission Policy*) - это API веб-платформы, который дает веб-сайту возможность разрешать или блокировать использование функций браузера в его собственном фрейме или в iframe, которые он встраивает. Он работает по принципу, согласно которому документы верхнего уровня, как правило, должны иметь доступ к мощным веб-функциям (часто по усмотрению пользователя, которому необходимо предоставить разрешение), но встроенный контент не должен получать такой доступ автоматически. Документ, который встраивает другой документ, должен иметь возможность указывать, какие функции он доверяет использовать этому встроенному контенту.

Примеры функций, которыми можно управлять с помощью политики разрешений, включают:

- [Battery status](https://w3c.github.io/battery/#permissions-policy-integration)
- [Client Hints](https://github.com/w3c/webappsec-permissions-policy/blob/main/permissions-policy-client-hints.md)
- Encrypted-media decoding
- [Fullscreen](https://fullscreen.spec.whatwg.org/#permissions-policy-integration)
- [Geolocation](https://w3c.github.io/geolocation-api/#permissions-policy)
- [Picture-in-picture](https://w3c.github.io/picture-in-picture/#permissions-policy)
- [Sensors](https://w3c.github.io/sensors/#permissions-policy): Accelerometer, Ambient Light Sensor, Gyroscope, Magnetometer
- [User media](https://w3c.github.io/mediacapture-main/#permissions-policy-integration): Camera, Microphone
- [Video Autoplay](https://html.spec.whatwg.org/multipage/infrastructure.html#autoplay-feature)
- [Web Payment Request](https://w3c.github.io/payment-request/#permissions-policy)
- [WebMIDI](https://webaudio.github.io/web-midi-api/#permissions-policy-integration)
- [WebUSB](https://wicg.github.io/webusb/#permissions-policy)
- [WebXR](https://immersive-web.github.io/webxr/#permissions-policy)

Полный список функций, которыми можно управлять с помощью политики разрешений доступен здесь: [Policy Controlled Features](https://github.com/w3c/webappsec-permissions-policy/blob/main/features.md)

### [Policy-controlled Features](https://w3c.github.io/webappsec-permissions-policy/#features)

Функция, управляемая политикой ([*policy-controlled feature*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature)), - это API или поведение, которые можно включить или отключить в документе, указав на них в [permissions policy](https://w3c.github.io/webappsec-permissions-policy/#permissions-policy).

Функции, управляемые политикой ([*policy-controlled feature*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature)), идентифицируются с помощью токенов (*tokens*), которые представляют собой строки, используемые в директивах политики ([*policy directives*](https://w3c.github.io/webappsec-permissions-policy/#policy-directive)).

Каждая функция, управляемая политикой ([*policy-controlled feature*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature)), имеет список разрешений по умолчанию ([*default allowlist*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature-default-allowlist)), который определяет, доступна ли эта функция в документах в переходных элементах верхнего уровня ([*top-level traversables*](https://html.spec.whatwg.org/multipage/document-sequences.html#top-level-traversable)) и как наследуется доступ к этой функции в дочерних навигационных объектах (*child navigables*).

Пользовательский агент (*user agent*) имеет набор поддерживаемых функций, то есть набор [функций](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature), которыми он позволяет управлять с помощью политик. Пользовательские агенты не обязаны поддерживать все [функции](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature).

### Allowlist

Список разрешений ([*allowlist*](https://w3c.github.io/webappsec-permissions-policy/#allowlist)) политики разрешений - это, по сути, набор источников ([*origins*](https://url.spec.whatwg.org/#concept-url-origin)). Список разрешений ([*allowlist*](https://w3c.github.io/webappsec-permissions-policy/#allowlist)) может быть:

При указании пустого списка источников в allowlist для указанной функции, функции будут отключены для всех документов, включая вложенные документы, независимо от их происхождения.

- `'none'`
- `*` (aka wildcard)
- **struct**
  - [**permissions-source-expression**](https://w3c.github.io/webappsec-permissions-policy/#permissions-source-expression)
    - [scheme-source](https://w3c.github.io/webappsec-csp/#grammardef-scheme-source) (как в CPS) - указывает источник, который соответствуют любому ресурсу, имеющему указанную схему. Например, "https:" / "custom-scheme:" / "another.custom-scheme:"
    - [host-source](https://w3c.github.io/webappsec-csp/#grammardef-host-source) (как в CPS) - например, "example.com" / "*.example.com" / "https://*.example.com:12/path/to/some"
  - [self-origin](https://w3c.github.io/webappsec-permissions-policy/#self-origin) - `'self'`
  - [src-origin](https://w3c.github.io/webappsec-permissions-policy/#src-origin) - `'src'`

Каждая функция, управляемая политикой, имеет список разрешений по умолчанию ([*default allowlist*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature-default-allowlist)).

## Header fields

### [`Permissions-Policy`](https://w3c.github.io/webappsec-permissions-policy/#permissions-policy-header) 🎩⬅️

**`Permissions-Policy`** - это HTTP-заголовок, который используется в ответе (*response*) для передачи политики разрешений ([*permissions policy*](https://w3c.github.io/webappsec-permissions-policy/#permissions-policy)), которая должна применяться клиентом.

```http

Permissions-Policy: geolocation=(self "https://example.com" "https://*.example.com")

Permissions-Policy: fullscreen=(), geolocation=()

```

### [`Permissions-Policy-Report-Only`](https://w3c.github.io/webappsec-permissions-policy/#permissions-policy-report-only-http-header-field) 🎩⬅️

## HTML and API's

### [allow attribute](https://w3c.github.io/webappsec-permissions-policy/#iframe-allow-attribute)

Элемент [`<iframe>`](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#the-iframe-element) имеет атрибут [`allow`](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#attr-iframe-allow), который содержит директивы политики в виде строки.

```html
<iframe
  src="https://example.com"
  allow="geolocation 'self' https://a.example.com https://b.example.com"></iframe>
```

### [interface PermissionsPolicy](https://w3c.github.io/webappsec-permissions-policy/#the-policy-object)

> [!CAUTION]
> Ситуация с JavaScript API's не понятна.
>
> Раньше Permission Policy называлась как Feature Policy. И с тех пор в Chrome API существует аттрибут `document.featurePolicy`,  при этом, в спецификация предлагает новый интерфейс `document.permissionsPolicy`, который пока (*05.05.24*) не доступен для вызова в Chrome и в других браузерах.
