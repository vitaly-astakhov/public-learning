# Referrer and Referrer policy

## [Referer](https://www.rfc-editor.org/rfc/rfc9110#name-referer) 🎩➡️🕵️

В названии поля, по историческим причинам, присутствует грамматическая ошибка.

- `Referer` - Это поле позволяет пользовательскому агенту (**user agent**), например браузеру, при переходе по ссылке передать новому ресурсу [absolute-URI](https://www.rfc-editor.org/rfc/rfc9110#uri.references) или [partial-URI](https://www.rfc-editor.org/rfc/rfc9110#uri.references), с которого был запрошен ресурс. То есть когда вы нажимаете на ссылку, ссылка содержит адрес страницы, на которую указана ссылка. Когда вы отправляете запросы ресурсов в другой домен, ссылка содержит адрес страницы, на которой используется запрашиваемый ресурс. Передачу этого поля контролирует политика **Referrer Policy**, [которая описана ниже](#referrer-policy).
- **Использование**: Эти данные могут быть использованы для аналитики, логирования, оптимизированного кэширования и т.д.

## Referrer Policy

<details>
<summary><b>enum ReferrerPolicy</b></summary>
<p>

[enum ReferrerPolicy](https://www.w3.org/TR/referrer-policy/#enumdef-referrerpolicy) {

- "" - пустая строка,
- `"no-referrer"` - Полностью запрещает передачу поля `Referer`
- `"no-referrer-when-downgrade"` - Запрещает передачу поля `Referer`, если использование TLS в [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) различается - передает весь URI.
- `"same-origin"`- Разрешает передачу поля `Referer`, только при навигации внутри одного источника (*origin*)
- `"origin"` - Передает только сам источник, без [путей](https://www.rfc-editor.org/rfc/rfc3986#section-3.3) - `scheme://host:port`
- `"strict-origin"` - Запрещает передачу поля `Referer`, если использование TLS в [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) различается - передает только сам источник, как описано выше
- `"origin-when-cross-origin"` - Передает полный URI при выполнении запроса с тем же источником (*origin*), но в других случаях отправляйте только источник (*origin*) документа.
- `"strict-origin-when-cross-origin"` (**DEFAULT**) - Запрещает передачу поля `Referer`, если использование TLS в [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) различается - передает полный URI при выполнении запроса с тем же источником (**origin**), но в других случаях отправляйте только источник (**origin**) документа
- `"unsafe-url"` - Разрешает передачу всем источникам

};

</p>
</details>

**Referrer-Policy** - это политика, которая изменяет алгоритм, используемый для заполнения заголовка `Referer` при [выборке (*fetching*)](https://fetch.spec.whatwg.org/#concept-fetch) подресурсов, предварительной выборке (**prefetching**) или выполнении навигации.

Управлять политикой передачи поля `Referrer` можно передать несколькими способами:

- Через HTTP заголовок `Referrer-Policy`, как описано [ниже](#referrer-policy-header)
- Через HTML элемент [`<meta/>`](https://html.spec.whatwg.org/multipage/semantics.html#meta) с аттрибутом `name`, который имеет значение [referrer](https://html.spec.whatwg.org/multipage/semantics.html#meta-referrer) (`name="referrer"`) и обязательным, для аттрибута `name`, аттрибутом `content`, чье значение должно соответствовать [ReferrerPolicy](https://w3c.github.io/webappsec-referrer-policy/#referrer-policy)
- Через атрибут `referrerpolicy` в HTML элементах: `<a/>`, `<area/>`, `<img/>`, `<iframe/>`, `<link/>` или `<script/>`.
- Через аттрибут `rel` со значением [`noreferrer`](https://html.spec.whatwg.org/multipage/semantics.html#link-type-noreferrer) (т.е. `rel="noreferrer"`) у ссылочных HTML элементов: `<a/>`, `<area/>`, `<form/>`.
- Неявно, через наследование. **Referrer policy** наследуется в соответствии с механизмом наследования [контейнеров политики](https://html.spec.whatwg.org/multipage/browsers.html#policy-container), определенным в спецификации HTML.

<details>
<summary>Зачем контролировать передачу поля Referer</summary>
<p>
[Источник примеров](https://w3c.github.io/webappsec-referrer-policy/#intro-privacy)

На сайте социальной сети есть страница профиля для каждого из ее пользователей, и пользователи добавляют гиперссылки со страницы своего профиля на свои любимые группы. Сайт социальной сети, возможно, не захочет передавать URL-адрес профиля пользователя на веб-сайты группы, когда другие пользователи переходят по этим гиперссылкам (поскольку URL-адреса профиля могут раскрыть личность владельца профиля).

Тем не менее, некоторые сайты социальных сетей могут захотеть проинформировать об этом веб-сайты группы что ссылки исходят с сайта социальной сети, но не раскрывают, какие именно Ссылки содержались в профиле конкретного пользователя.
</p>
</details>

### [Referrer-Policy](https://w3c.github.io/webappsec-referrer-policy/#referrer-policy) 🎩➡️ <a id="referrer-policy-header"/>

**Referrer-Policy** - это поле определяет **Referrer policy**, применяемую пользовательским агеном при определении того, какие сведения об отношениях следует включать в запросы и контексты просмотра, созданные в контексте защищенного ресурса.

___

При работе в HTML можно узнать кто referrer через аттрибут документа `document.referrer`. Подробнее: [HTML spec](https://html.spec.whatwg.org/multipage/dom.html#dom-document-referrer)
