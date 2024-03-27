# Referer

## [Referer](https://www.rfc-editor.org/rfc/rfc9110#name-referer) (Отправляется только агентом пользователя)  🎩
- **Referer** - Это поле позволяет агенту пользователя (**user agent**), например браузеру, при переходе по ссылке передать новому ресурсу [absolute-URI](https://www.rfc-editor.org/rfc/rfc9110#uri.references) или [partial-URI](https://www.rfc-editor.org/rfc/rfc9110#uri.references), с которого был запрошен ресурс. То есть когда вы нажимаете на ссылку, ссылка содержит адрес страницы, на которую указана ссылка. Когда вы отправляете запросы ресурсов в другой домен, ссылка содержит адрес страницы, на которой используется запрашиваемый ресурс.
- **Использование**: Эти данные могут быть использованы для аналитики, логирования, оптимизированного кэширования и т.д.

Передача и область применения этого поля **_Referer_** может регулироваться заголовком заголовком [**Referrer Policy**](https://w3c.github.io/webappsec-referrer-policy). Может так же регулироваться HTML аттрибутом [rel](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel) со значением [noreferrer](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel/noreferrer)

<details><summary>Для чего вообще нужно/можно регулировать передачу поля Referer</summary>
<p>
[Источник примеров](https://w3c.github.io/webappsec-referrer-policy/#intro-privacy)

На сайте социальной сети есть страница профиля для каждого из ее пользователей, и пользователи добавляют гиперссылки со страницы своего профиля на свои любимые группы. Сайт социальной сети, возможно, не захочет передавать URL-адрес профиля пользователя на веб-сайты группы, когда другие пользователи переходят по этим гиперссылкам (поскольку URL-адреса профиля могут раскрыть личность владельца профиля).

Тем не менее, некоторые сайты социальных сетей могут захотеть проинформировать об этом веб-сайты группы что ссылки исходят с сайта социальной сети, но не раскрывают, какие именно Ссылки содержались в профиле конкретного пользователя.
</p>
</details>

### [Referrer-Policy](https://w3c.github.io/webappsec-referrer-policy/#referrer-policy) 🎩

**Referrer-Policy** - это поле изменяет алгоритм, используемый для полем [**Referer**](https://www.rfc-editor.org/rfc/rfc9110#name-referer) при [получении (**fetching**)](https://fetch.spec.whatwg.org/#concept-fetch) вложенных ресурсов, предварительной выборке (**prefetching**) или выполнении навигации.
**Referrer-Policy** по умолчанию содержит значение "strict-origin-when-cross-origin".

Это поле можно передать несколькими способами:
- Через заголовок `Referrer-Policy`, как было описано выше
- Через HTML [мета-элемент](https://html.spec.whatwg.org/multipage/semantics.html#meta) с именем [referrer](https://html.spec.whatwg.org/multipage/semantics.html#meta-referrer).
- Через атрибут referrerpolicy для элементов: `<a/>`, `<area/>`, `<img/>`, `<iframe/>`, `<link/>` или `<script/>`.
- Через отношение [noreferrer](https://html.spec.whatwg.org/multipage/semantics.html#link-type-noreferrer) link для элемента `<a/>`или `<area/>`.
- Неявно, через наследование - Referrer policy наследуется в соответствии с механизмом наследования [контейнеров политики](https://html.spec.whatwg.org/multipage/browsers.html#policy-container), определенным в HTML.

<details><summary>Значение, которые можно передать в поле Referrer-Policy</summary>
<p>

enum ReferrerPolicy {
  "",
  "no-referrer", // Запрещает передачу поля **Referer**
  "no-referrer-when-downgrade", // Запрещает передачу поля **Referer**, если использование TLS в [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) различается - передает весь URI.
  "same-origin", // Разрешает передачу поля **Referer*, только при навигации внутри одного источника (**origin**)
  "origin", // Передает только сам источник, без [путей](https://www.rfc-editor.org/rfc/rfc3986#section-3.3) - `scheme://host:port`
  "strict-origin", //  Запрещает передачу поля **Referer**, если использование TLS в [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) различается - передает только сам источник, как описано выше
  "origin-when-cross-origin", // Передает полный URI при выполнении запроса с тем же источником (**origin**), но в других случаях отправляйте только источник (**origin**) документа.
  "strict-origin-when-cross-origin" (**default**), Запрещает передачу поля **Referer**, если использование TLS в [URI scheme](https://www.rfc-editor.org/rfc/rfc3986#section-3.1) различается - передает полный URI при выполнении запроса с тем же источником (**origin**), но в других случаях отправляйте только источник (**origin**) документа
  "unsafe-url" // Разрешает передачу всем источникам
};

</p>
</details>
