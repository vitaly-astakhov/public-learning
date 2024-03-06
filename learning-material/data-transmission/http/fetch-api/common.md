#

### URL

Локальная схема - это "about", "blob" или "data".

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
