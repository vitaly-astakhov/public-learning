# Scripts

## [Script processing model](https://html.spec.whatwg.org/multipage/webappapis.html#scripting-processing-model)

Скрипт - это одна из двух возможных структур (а именно, классический скрипт или модульный скрипт).

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

Модульные скрипты можно разделить на три типа:

- [**JavaScript module script**](https://html.spec.whatwg.org/multipage/webappapis.html#javascript-module-script)
- [**CSS module script**](https://html.spec.whatwg.org/multipage/webappapis.html#css-module-script)
- [**JSON module script**](https://html.spec.whatwg.org/multipage/webappapis.html#json-module-script)
