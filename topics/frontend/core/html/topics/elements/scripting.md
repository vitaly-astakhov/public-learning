# [Scripting](https://html.spec.whatwg.org/multipage/scripting.html#scripting-3)

## Navigation

- [`<script> element`](#script-element)
- [`<noscript> element`](#noscript-element)
- [`<template> element`](#template-element)
- [`<slot> element`](#slot-element)

___

## Script

Скрипт - это одна из двух возможных структур

- классический скрипт ([*classic script*](https://html.spec.whatwg.org/multipage/webappapis.html#classic-script))
- модульный скрипт ([*module script*](https://html.spec.whatwg.org/multipage/webappapis.html#module-script)).

Все скрипты имеют:

- [**settings object**](https://html.spec.whatwg.org/multipage/webappapis.html#settings-object) - Объект настроек среды (*[environment settings object](https://html.spec.whatwg.org/multipage/webappapis.html#environment-settings-object)*), содержащий различные настройки, которые используются другими скриптами в том же контексте.
- [**record**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-script-record) - одно из следующих
  - [script record](https://tc39.es/ecma262/#sec-script-records), for [classic scripts](https://html.spec.whatwg.org/multipage/webappapis.html#classic-script);
  - [Source Text Module Record](https://tc39.es/ecma262/#sec-source-text-module-records), for [JavaScript module scripts](https://html.spec.whatwg.org/multipage/webappapis.html#javascript-module-script);
  - [Synthetic Module Record](https://tc39.es/proposal-json-modules/#sec-synthetic-module-records), for [CSS module scripts](https://html.spec.whatwg.org/multipage/webappapis.html#css-module-script) and [JSON module scripts](https://html.spec.whatwg.org/multipage/webappapis.html#json-module-script)
  - null, representing a parsing failure.
- [**parse error**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-script-parse-error) - Значение JavaScript, которое имеет значение только в том случае, если запись (**record**) равна null, указывающее на то, что соответствующий исходный текст скрипта не удалось проанализировать. Это значение используется для внутреннего отслеживания ошибок немедленного синтаксического анализа при создании скриптов и не должно использоваться напрямую.
- [**error to rethrow**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-script-error-to-rethrow)
- [Fetch options](https://html.spec.whatwg.org/multipage/webappapis.html#concept-script-script-fetch-options)
- [**base URL**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-script-base-url)

Скрипты позволяют авторам добавлять интерактивность в свои документы.

Авторам рекомендуется по возможности использовать декларативные альтернативы использованию сценариев, поскольку декларативные механизмы часто более удобны в обслуживании, и многие пользователи отключают использование сценариев.

Например, вместо использования скриптов для отображения или скрытия раздела для отображения более подробной информации можно использовать элемент [`<details>`](https://html.spec.whatwg.org/multipage/interactive-elements.html#the-details-element).

## [`<script>` element](https://html.spec.whatwg.org/multipage/scripting.html#the-script-element) 🏷️ <a id="script-element" />

Элемент **`<script>`** позволяет авторам включать динамические сценарии/скрипты (*scripts*) и блоки данных в свои документы. Этот элемент не представляет контент для пользователя.

### Types

Атрибут `type` позволяет настраивать тип представленного скрипта.

Авторам следует опустить атрибут `type` вместо того, чтобы устанавливать его избыточно.

- [**classic script**](https://html.spec.whatwg.org/multipage/webappapis.html#classic-script) - скрипт является "классическим", если аттрибут `type` не будет установлен для элемента. Такой скрипт должен интерпретироваться в соответствии с алгоритмами [JavaScript Script](https://tc39.es/ecma262/multipage/ecmascript-language-scripts-and-modules.html#prod-Script). Атрибуты `async` и `defer` влияют на классические скрипты, но только в том случае, если установлен атрибут `src`.
- [**javascript module script**](https://html.spec.whatwg.org/multipage/webappapis.html#javascript-module-script) - скрипт является "модульный", если аттрибут `type` будет иметь значение `module`, т.е `type=module`. Такой скрипт должен интерпретироваться в соответствии с алгоритмами [JavaScript Module Script](https://tc39.es/ecma262/multipage/ecmascript-language-scripts-and-modules.html#prod-Module). На модульные скрипты не влияет атрибут `defer`, но влияет атрибут `async` (независимо от состояния атрибута `src`).
- [**import map**](https://html.spec.whatwg.org/multipage/webappapis.html#import-map) - скрипт будет представлять собой карту импорта ([*import map*](https://html.spec.whatwg.org/multipage/webappapis.html#import-map)), содержащую JSON, которая будет использоваться для управления поведением разрешения спецификатора модуля, если аттрибут `type` будет иметь значение `importmap`. Импортировать карты можно только встроенными, т.е. атрибут `src` и большинство других атрибутов не имеют смысла и не должны использоваться с ними. Документ не должен содержать более одного элемента сценария импорта карты ([*import map*](https://html.spec.whatwg.org/multipage/webappapis.html#import-map)).
- **speculationrules**
- [**data block**](https://html.spec.whatwg.org/multipage/scripting.html#data-block) - Authors must use a [valid MIME type string](https://mimesniff.spec.whatwg.org/#valid-mime-type) that is not a [JavaScript MIME type essence match](https://mimesniff.spec.whatwg.org/#javascript-mime-type-essence-match) to denote data blocks.

Классические скрипты (*classic script*) и скрипты модуля JavaScript (*JavaScript module script*) могут быть встроены в систему (*embedded inline*) или импортированы из внешнего файла с использованием атрибута `src`,

Модульные скрипты можно разделить на три типа:

#### [**JavaScript module script**](https://html.spec.whatwg.org/multipage/webappapis.html#javascript-module-script)

```javascript
import format from './format.js';
```

#### [**CSS module script**](https://html.spec.whatwg.org/multipage/webappapis.html#css-module-script)

```javascript
import sheet from './styles.css' with { type: 'css' };
```

#### [**JSON module script**](https://html.spec.whatwg.org/multipage/webappapis.html#json-module-script)

```javascript
import peopleInSpace from "http://api.open-notify.org/astros.json" with { type: "json" };
```

### Script loading and evaluating

Атрибуты `async` и `defer` являются логическими атрибутами (*boolean*), которые указывают, как следует загружать и выполнять скрипт.

- [**`async`**](https://html.spec.whatwg.org/multipage/scripting.html#attr-script-async) - позволяет скрипту выполняться, как только он станет доступен, без ожидания завершения парсинга документа. Если присутствует атрибут **`async`**, скрипт будет загружен параллельно с парсингом и выполнен, как только он станет доступен, что может произойти до завершения парсинга. Имеет приоритет над аттрибутом `defer`.
- [**`defer`**](https://html.spec.whatwg.org/multipage/scripting.html#attr-script-defer) - откладывает выполнение (*execution*) скрипта до тех пор, пока не завершится парсинг документа. Модульные скрипты (`type="module"`) по умолчанию загружаются так, как если бы у них был атрибут **`defer`**.

Если ни один из атрибутов не присутствует, скрипт будет загружен (*fetched*)  и выполнен (*executed*) немедленно, блокируя парсинг документа до тех пор, пока обе операции не будут завершены.

![asyncdefer](../../assets/asyncdefer.svg)
Источник: <https://html.spec.whatwg.org/images/asyncdefer.svg>

## [`<noscript>` element](https://html.spec.whatwg.org/multipage/scripting.html#the-noscript-element)

Элемент **`<noscript>`** ничего не представляет, если включен scripting ([*scripting is enabled*](https://html.spec.whatwg.org/multipage/webappapis.html#concept-n-script),), и представляет его дочерние элементы, если scripting отключен ([scripting is disabled](https://html.spec.whatwg.org/multipage/webappapis.html#concept-n-noscript)).

## [`<template>` element](https://html.spec.whatwg.org/multipage/scripting.html#the-template-element) 🏷️ <a id="template-element" />

Элемент **`<template>`** используется для объявления фрагментов HTML, которые могут быть клонированы и вставлены в документ с помощью скрипта. При рендеринге элемент **`<template>`** ничего не представляет.

## [`<slot>` element](https://html.spec.whatwg.org/multipage/scripting.html#the-slot-element) 🏷️ <a id="slot-element" />

Элемент **`<slot>`** определяет [слот](https://dom.spec.whatwg.org/#concept-slot). Обычно он используется в теневом дереве ([*shadow tree*](https://dom.spec.whatwg.org/#concept-shadow-tree)). Элемент **`<slot>`** представляет назначенные ему узлы ([*assigned nodes*](https://dom.spec.whatwg.org/#slot-assigned-nodes)), если таковые имеются, и его содержимое в противном случае.
