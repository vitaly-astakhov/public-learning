# Early Hints (Ранние подсказки)

## Documentation

- [IETF RFC 8297 An HTTP Status Code for Indicating Hints](https://datatracker.ietf.org/doc/html/rfc8297)
- [WHATWG - HTML Spec - Early hints](https://html.spec.whatwg.org/multipage/semantics.html#early-hints)

## Articles

- [ ] [Early Hints Support on Navigation Responses](https://docs.google.com/document/d/1gCh_CnfrJq_VL7aGoq6skc7sn4yn5pKsM0gkHe5B9go/edit#heading=h.yh1rfx1p5ocs)

## Debug Tools

- [Check for 103 Early Hints](https://code103.hotmann.de/)

## Some

- [example](https://early-hints.fastlylabs.com/)

## Overview

Ранние подсказки (**Early Hints**) позволяют пользовательским агентам (*user agent*) выполнять некоторые операции, такие как предположительная загрузка ресурсов (*speculatively load resources*), которые, вероятно, будут использоваться документом, до того, как запрос навигации будет полностью обработан сервером и будет отправлен код ответа. Например, клиент может распознать значение поля заголовка `[Link](https://httpwg.org/specs/rfc8288.html#header)`, содержащее тип отношения [`preload`](https://html.spec.whatwg.org/multipage/links.html#link-type-preload), и начать получение целевого ресурса. Серверы могут указывать на ранние подсказки, отправляя ответ с необходимыми полями и кодом состояния [`103 (Early Hints)`](https://www.rfc-editor.org/rfc/rfc8297#section-2) перед отправкой окончательного ответа.

Сервер **МОЖЕТ (MAY)** использовать ответ [`103 (Early Hints)`](https://www.rfc-editor.org/rfc/rfc8297#section-2), чтобы указать только некоторые поля заголовка, которые, как ожидается, будут найдены в окончательном ответе. Клиент **НЕ ДОЛЖЕН (MUST NOT)** интерпретировать отсутствие поля заголовка в ответе [`103 (Early Hints)`](https://www.rfc-editor.org/rfc/rfc8297#section-2) как предположение о том, что поле заголовка вряд ли будет частью окончательного ответа.

Сервер **МОЖЕТ (MAY)** выдать несколько ответов [`103 (Early Hints)`](https://www.rfc-editor.org/rfc/rfc8297#section-2) с дополнительными полями заголовка, когда новая информация становится доступной во время обработки запроса. Ему не нужно повторять уже созданные поля, но и не нужно их исключать. Клиент может учитывать любую комбинацию полей заголовков, полученных в нескольких ответах [`103 (Early Hints)`](https://www.rfc-editor.org/rfc/rfc8297#section-2), при ожидании списка полей заголовков, ожидаемых в окончательном ответе.

В дополнение к полю заголовка `[Link](https://httpwg.org/specs/rfc8288.html#header)`, возможно, что ответ [`103 (Early Hints)`](https://www.rfc-editor.org/rfc/rfc8297#section-2), содержит заголовок [`Content Security Policy`](https://w3c.github.io/webappsec-csp/#content-security-policy-object), который применяется при обработке ранней подсказки.
