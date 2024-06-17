# Permissions

## Materials

### Documentation

- [Permissions](https://w3c.github.io/permissions)

## Table of contents

- [Overview](#overview)
  - [Powerful features](#powerful-features)
  - [Permissions API](#permissions-api)
- [Permissions Policy 📂](../../../../../communication/http/topics/policies/permissions-policy.md)
- [Examples of Permissions API usage 📂](./examples/example-permissions.md)

## Overview

Разрешение (*permission*) отражает текущее состояние согласия (*consent*) пользователя на определенные типы функций, в частности на "мощные функции" ([*powerful features*](https://w3c.github.io/permissions/#dfn-powerful-feature)). В конечном счете, пользователь сохраняет контроль над этими разрешениями (*permissions*) и может вручную предоставлять (*grant*) или отклонять (*deny*) разрешения (*permissions*) через настройки пользователя. Кроме того, пользовательские агенты (*user agent*) помогают пользователям управлять разрешениями (*permissions*), например, скрывая и автоматически отклоняя определенные запросы на получение разрешений (*permission*), которые в противном случае были бы неприятными, и автоматически аннулируя предоставленные разрешения, если пользователь не посещает веб-сайт в течение некоторого времени.

Концептуально, разрешение на использование мощной функции ([*powerful feature*](https://w3c.github.io/permissions/#dfn-powerful-feature)) может находиться в одном из следующих состояний:

- ["denied"](https://w3c.github.io/permissions/#dfn-denied) - Пользователь или пользовательский агент от имени пользователя отказал в доступе (*has denied access*) к этой мощной функции (*powerful feature*).
- ["granted"](https://w3c.github.io/permissions/#dfn-granted) - Пользователь или пользовательский агент от имени пользователя дал явное разрешение ([*express permission*](https://w3c.github.io/permissions/#dfn-express-permission)) на использование мощной функции (*powerful feature*).
- ["prompt"](https://w3c.github.io/permissions/#dfn-prompt) (**default**) - Пользователь не давал явного разрешения на использование этой функции (т.е. это то же самое, что ["denied"](https://w3c.github.io/permissions/#dfn-denied)). Это также означает, что если вызывающий абонент попытается воспользоваться функцией, пользовательский агент либо запросит у пользователя разрешение, либо доступ к функции будет "запрещен".

### Powerful features

Мощная функция ([*powerful feature*](https://w3c.github.io/permissions/#dfn-powerful-feature)) - это функция веб-платформы (обычно API), для использования которой пользователь дает явное разрешение [*express permission*](https://w3c.github.io/permissions/#dfn-express-permission). За исключением нескольких заметных исключений (например, [*Notifications API Standard*](https://notifications.spec.whatwg.org/)), большинство мощных функций (*powerful feature*) также являются функциями, управляемыми политикой ([*policy-controlled features*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature)). Для мощных функций (*powerful features*), которые также управляются политикой ([*policy-controlled features*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature)), определяет, разрешено ли документу ([*document*](https://dom.spec.whatwg.org/#concept-document)) использовать ту ([*allowed to use*](https://html.spec.whatwg.org/multipage/iframe-embed-object.html#allowed-to-use)) или иную функцию. То есть мощная функция (*powerful feature*) может запрашивать явное разрешение у пользователя ([*express permission*](https://w3c.github.io/permissions/#dfn-express-permission)) только в том случае, если документу ([*document*](https://dom.spec.whatwg.org/#concept-document)) делегировано разрешение с помощью соответствующей функции, управляемой политикой ([*policy-controlled features*](https://w3c.github.io/webappsec-permissions-policy/#policy-controlled-feature)). Последующий доступ (*subsequent access*) к функции определяется наличием у пользователя "предоставленного" ([*granted*](https://w3c.github.io/permissions/#dfn-granted)) разрешения или соответствием некоторым критериям, которые эквивалентны предоставлению разрешения ([*grant permission*](https://w3c.github.io/permissions/#dfn-granted)).

Мощная функция (*powerful feature*) идентифицируется по ее [названию](https://w3c.github.io/permissions/#dfn-name), которое представляет собой строковый литерал (например, "geolocation").

## Permissions API

Доступ к интерфейсу [Permissions](https://w3c.github.io/permissions/#permissions-interface) можно получить через аттрибут [`navigator.permissions`](https://w3c.github.io/permissions/#dom-navigator-permissions), так как Permissions API является расширением для интерфейсов [Navigator](https://html.spec.whatwg.org/multipage/system-state.html#navigator) и [WorkerNavigator](https://html.spec.whatwg.org/multipage/workers.html#workernavigator).

Интерфейс [Permissions](https://w3c.github.io/permissions/#permissions-interface) содержит пока только один метод [`query()`](https://w3c.github.io/permissions/#query-method), который возвращает Promise, который в себе содержит [PermissionStatus interface](https://w3c.github.io/permissions/#permissionstatus-interface).

[PermissionStatus interface](https://w3c.github.io/permissions/#permissionstatus-interface) содержит несколько аттрибутов:

- [`state`](https://w3c.github.io/permissions/#dom-permissionstatus-state)
  - ["granted"](https://w3c.github.io/permissions/#dfn-granted),
  - ["denied"](https://w3c.github.io/permissions/#dfn-denied),
  - ["prompt"](https://w3c.github.io/permissions/#dfn-prompt) ([default](https://w3c.github.io/permissions/#dfn-default-state))
- [`name`](https://w3c.github.io/permissions/#dom-permissionstatus-name)
- [`onchange`](https://w3c.github.io/permissions/#dom-permissionstatus-onchange)
