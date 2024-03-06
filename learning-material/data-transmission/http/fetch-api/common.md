#

### URL

**Local scheme (локальная схема)** - это "about", "blob" или "data".

URL-адрес является локальным, если его схема является локальной схемой.

**HTTP(S) scheme** — «http» или «https».

**Fetch scheme** — это **local scheme**, "file" или **HTTP(S) scheme**.

## HTTP

### [Methods](https://fetch.spec.whatwg.org/#methods)

Методы, которые запрещены (**forbidden method**) для использования в Fetch API : `CONNECT`, `TRACE`.

Нормализация - это процесс приведения методов, к uppercase формату. Это делается Fetch API, так как методы на самом деле "чувствительны к регистру" (case-sensitive).

### [Headers](https://fetch.spec.whatwg.org/#terminology-headers)

HTTP обычно называет заголовок «полем» (**field**) или «полем заголовка» (**header field**). Веб-платформа использует более разговорный термин «заголовок».

Если при отправки сообщения встречаются поля с одинаковым названием, то их значения комбинируются в одно поле.

В **Fetch API** заголовки сортируются по возрастанию. Источник: https://fetch.spec.whatwg.org/#concept-header-list-sort-and-combine

<details>
<summary>Пример сортировкой заголовков и комбинирования полей:</summary>
<p>

```javascript
// Заголовки, которые пойдут потом пойдут в fetch

const headers = new Headers([
  ["Header-1", "value 1"],
  ["Header-3", "value 3"],
  ["Header-2", "value 2"],
  ["Header-3", "value 4"],
]);
```
Получаемый результат будет такой:

![Результат сортировки заголовков и комбинирования полей](../assets/fetch-api/20240305211730.png)

</p>
</details>

### [Forbidden request-header](https://fetch.spec.whatwg.org/#forbidden-request-header)

Это поля считаются запрещенными, так что их нельзя добавить или изменен программно, поэтому пользовательский агент сохраняет полный контроль над ними.

- `Accept-Charset`
- `Accept-Encoding`
- `Access-Control-Request-Headers`
- `Access-Control-Request-Method`
- `Connection`
- [`Content-Length`](https://www.rfc-editor.org/rfc/rfc9110#name-content-length)
- `Cookie`
- `Cookie2`
- `Date`
- `DNT`
- `Expect`
- `Host`
- `Keep-Alive`
- `Origin`
- `Referer`
- `TE`
- `Trailer`
- `Transfer-Encoding`
- `Upgrade`
- `Via`
- `Set-Cookie`
- `Proxy-`
- `Sec-`

### [Forbidden response-header name](https://fetch.spec.whatwg.org/#forbidden-response-header-name)
- `Set-Cookie`
- `Set-Cookie2`


## [Statuses](https://fetch.spec.whatwg.org/#statuses)

**Fetch API** работает только со статусами в диапазоне от 0 до 999

**Fetch API** разделяет статусы на категории:
- [**null body status**](https://fetch.spec.whatwg.org/#null-body-status) - статусы `101`, `103`, `204`, `205`, `304`.
- [**ok status**](https://fetch.spec.whatwg.org/#ok-status) - статусы диапазона от 200 до 299
- [**redirect status**](https://fetch.spec.whatwg.org/#redirect-status) - статусы `301`, `302`, `303`, `307`, `308`.
