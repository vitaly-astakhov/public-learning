# Methods (HTTP verbs)

## Table of contents

- [Methods (HTTP verbs)](#methods-http-verbs)
  - [Table of contents](#table-of-contents)
  - [Overview](#overview)
    - [Method safeness](#method-safeness)
    - [Idempotency](#idempotency)
  - [Methods](#methods)
    - [`OPTIONS`](#options)
    - [`GET`](#get)
    - [`HEAD`](#head)
    - [`POST`](#post)
    - [`PUT`](#put)
    - [`PATCH`](#patch)
    - [`DELETE`](#delete)
    - [`CONNECT`](#connect)
    - [`TRACE`](#trace)
  - [Notes](#notes)
    - [Example of passing `PUT` method within HTTP body 📂](#example-of-passing-put-method-within-http-body-)

## Overview

**Request method** - часть request семантики и указывает на цель/действие, с которой клиент сделал этот запрос, и что ожидается клиентом в качестве успешного результата.

Request method вызывает действие, которое должно быть применено к целевому ресурсу.

Стандартные методы: `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE`.

Нестандартные, но зарегистрированные методы: [`PATCH`](https://www.rfc-editor.org/rfc/rfc5789), `PRI` (HTTP/2)

### Method safeness

Методы считаются **безопасными (*safe*)**, если их семантика означает только доступ к чтению целевого ресурса. Безопасными методами являются: `GET`, `HEAD`, `OPTIONS`, and `TRACE`. [^1]

Цель проведения различия между безопасными и небезопасными методами состоит в том, чтобы позволить автоматизированным процессам поиска (spiders, web-crawlers) и оптимизации производительности кэша (предварительная выборка - pre-fetching) работать, не опасаясь причинения вреда.

Больше информации можно найти тут: <https://www.rfc-editor.org/rfc/rfc9110#name-safe-methods>

### Idempotency

[Идемпотентный метод](https://www.rfc-editor.org/rfc/rfc9110#name-idempotent-methods) - это метод, который может быть вызван много раз без разных результатов. Не должно иметь значения, был ли метод вызван только один раз или более десяти раз. Результат всегда должен быть одинаковым.
Идемпотентными методами являются: `PUT`,`DELETE`. Так же идемпотентными методами считаются "безопасные" методы:`GET`,`HEAD`,`OPTIONS`,`TRACE`.

Метод `POST` не импотентный так как он обычно, но не обязательно, используются для создания нового ресурса на сервере. Таким образом, когда мы выполняем один и тот же `POST` запрос N-количество раз, у нас будет N-количество новых ресурсов на сервере.

## Methods

### [`OPTIONS`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.7)

[`OPTIONS`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.7) - ОПЦИИ

- **Команда серверу**: Опиши опции (`options`) взаимодействия с целевым ресурсом.
- **Описание**: Метод `OPTIONS` запрашивает сведения о параметрах (опциях) связи доступен для целевого ресурса, либо на сервере-источнике, либо на посредника. Этот метод позволяет клиенту определить параметры (опции) и/или требования, связанные с ресурсом или возможностями сервера, не подразумевая действия с ресурсом.
- **Использование**: используется для идентификации (узнавания) у сервера, какие другие методы, т.е. опции (`options`), он принимает.
- **Возвращает**: сервер **ДОЛЖЕН (SHOULD)** вернуть любой заголовок (**header**), который может указывать на дополнительные функции (опции), реализованные сервером и применимые к целевому ресурсу (например, [`Allow`](https://www.rfc-editor.org/rfc/rfc9110#field.allow). Так же может вернуть и другие заголовки.

<details>
<summary>Запрос `OPTIONS` со звездочкой ("*" - asterisk form) в качестве цели запроса</summary>
<p>

Запрос `OPTIONS` со звездочкой ("*" - asterisk form) в качестве цели запроса ([Раздел 7.1](https://www.rfc-editor.org/rfc/rfc9110#target.resource)) применяется к серверу в целом, а не к специфического ресурса.

Если целью запроса не является ("*" - asterisk form), применяется запрос `OPTIONS` к опциям, которые доступны при общении с целевым ресурсом

[Источник](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.7-2).

> [!WARNING]
> Не работает в **Fetch API**.[^2][^3]

</p>
</details>

### [`GET`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.1)

[`GET`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.1) - ПОЛУЧИТЬ

- **Команда серверу**: Перенесите текущее представление целевого ресурса.
- **Описание**: Метод `GET` запрашивает у сервера-источника передачу текущего [выбранного представления](https://www.rfc-editor.org/rfc/rfc9110#selected.representation) для [целевого ресурса](https://www.rfc-editor.org/rfc/rfc9110#target.resource)
- **Возвращает**: заголовки (**headers**), и содержимое (**content**) целевого ресурса.

### [`HEAD`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.2)

[`HEAD`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.2) - ЗАГОЛОВКИ (я думаю, что название метода `HEAD` происходит от слова headers, то есть заголовки)

- **Команда серверу**: Перенесите текущее представление целевого ресурса, но без контента.
- **Описание**: Метод `HEAD` запрашивает у сервера-источника передачу текущего [выбранного представления](https://www.rfc-editor.org/rfc/rfc9110#selected.representation) для [целевого ресурса](https://www.rfc-editor.org/rfc/rfc9110#target.resource), без содержимого
- **Возвращает**: заголовки (**headers**), и НЕ ВОЗВРАЩАЕТ содержимое (**content**) целевого ресурса.

### [`POST`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.3)

 [`POST`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.3) - ОТПРАВИТЬ

- **Команда серверу**: Выполните обработку содержимого (**content**) запроса, зависящую от конкретного ресурса
- **Описание**: Метод `POST` запрашивает, чтобы целевой ресурс обработал представление, заключенное в запросе
- **Использование**: Используется для отправки данных к определённому ресурсу сервера. Используется для создание нового ресурса, который еще не идентифицирован. Часто вызывает изменение состояния или какие-то побочные эффекты на сервере.
- **Возвращает**: заголовки (**headers**) и содержимое (**content**)

### [`PUT`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.4)

[`PUT`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.4) - ЗАМЕНИТЬ (перевод как будто не совсем корректный)

- **Команда серверу**: замени все текущие представления (representation) целевого ресурса (target resource) содержимым (**content**) запроса.
- **Описание**: Метод `PUT` запрашивает (**request**) у сервера-источника создание или замену состояния [целевого ресурса](https://www.rfc-editor.org/rfc/rfc9110#target.resource) состоянием, определенным представлением в содержимое сообщения запроса.
- **Использование**:
  - Используется для замены текущих данных ресурсов сервера на новые, передаваемые запросом. То есть полностью заменяет запись на сервере.
  - Если ресурс в момента запроса (**request**) с методом `PUT` не существует, то сервер-источник может создать такой ресурс и **ДОЛЖЕН (MUST)** сообщить агенту пользователя (**user agent**), отправив ответ [201 (Created).](https://www.rfc-editor.org/rfc/rfc9110#status.201)
- **Принимает**: желаемое состояние [целевого ресурса](https://www.rfc-editor.org/rfc/rfc9110#target.resource) , которое после успешного применения запроса `PUT`, заменит существующее состояние ресурса или создаст другой ресурс
- **Возвращает**: заголовки (**headers**) и содержимое (**content**)

Метод `PUT` предполагает, что клиент знает, какой ресурс он хочет обновить. Если сервер не может обновить запрашиваемый ресурс и хочет, чтобы клиент обновил другой ресурс, например, если ресурс был перемещен на другой URI, то сервер **ДОЛЖЕН (MUST)** отправить подходящий ответ с кодом [3xx (Redirection)](https://www.rfc-editor.org/rfc/rfc9110#section-15.4); клиент **МОЖЕТ (MAY)** тогда сам решить, следует ли перенаправить запрос или нет.

### [`PATCH`](https://www.rfc-editor.org/rfc/rfc5789#section-2)

[PATCH](https://www.rfc-editor.org/rfc/rfc5789#section-2) - ИСПРАВЛЕНИЕ

- **Описание**: Метод `PATCH` запрашивает (**request**) у сервера-источника изменение состояния [целевого ресурса](https://www.rfc-editor.org/rfc/rfc9110#target.resource) состоянием, определенным представлением в содержимое сообщения запроса. В отличие от `PUT`, `PATCH` этот метод содержит набор инструкций, описывающих, как изменить текущий ресурс для создания новой версии. Это можно сравнить с исправлением опечаток в книге, не заменяя всю книгу целиком.
- **Использование**:
  - Используется для частичного изменения ресурса сервера без замены всего ресурса. как это делает `PUT`.
  - Если ресурс в момента запроса (**request**) с методом `PATCH` не существует, то сервер-источник может создать такой ресурс и **ДОЛЖЕН (SHOULD)** сообщить агенту пользователя (**user agent**), отправив ответ [201 (Created).](https://www.rfc-editor.org/rfc/rfc9110#status.201)
- **Принимает**: желаемое для замены состояние [целевого ресурса](https://www.rfc-editor.org/rfc/rfc9110#target.resource), которое после успешного применения запроса `PATCH`, частично обновит существующее состояние ресурса или создаст другой ресурс.

<details>
<summary>Тонкости в использовании метода PATCH</summary>
<p>

Clients need to choose when to use `PATCH` rather than `PUT`. For
example, if the patch document size is larger than the size of the
new resource data that would be used in a `PUT`, then it might make
sense to use `PUT` instead of `PATCH`. A comparison to `POST` is even more
difficult, because `POST` is used in widely varying ways and can
encompass `PUT` and `PATCH`-like operations if the server chooses. If
the operation does not modify the resource identified by the Request-
URI in a predictable way, `POST` should be considered instead of `PATCH`
or `PUT`.

[Источник](https://www.rfc-editor.org/rfc/rfc5789#:~:text=Clients%20need%20to%20choose%20when,or%20PUT).

</p>
</details>

<details>
<summary>Отличие метода PUT от PATCH - GPT4</summary>
<p>

- `PUT`: Этот метод используется для полной замены ресурса на сервере. Если вы отправляете `PUT`-запрос, то вы предоставляете обновленную версию ресурса, которая полностью заменит текущую версию на сервере. Это похоже на то, как если бы вы заменили старую книгу на полке новым изданием.
- `PATCH`: В отличие от `PUT`, `PATCH` применяется для частичного обновления ресурса. Этот метод содержит набор инструкций, описывающих, как изменить текущий ресурс для создания новой версии. Это можно сравнить с исправлением опечаток в книге, не заменяя всю книгу целиком.

</p>
</details>

<details>
<summary>Заголовки, которые относятся только к PATCH</summary>
<p>

[`Accept-Patch`](https://www.rfc-editor.org/rfc/rfc5789#section-3.1) - Определяет принятые форматы исправлений для документов. Должен отправляться вместе с ответом (**response**) при вызове запроса с методом **`OPTIONS`**

</p>
</details>

### [`DELETE`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.5)

 [`DELETE`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.5) - УДАЛИТЬ

- **Команда серверу**: Удалите все текущие представления целевого ресурса.
- **Описание**: Метод `DELETE` запрашивает у сервера-источника (**origin server**) удаление связи между [целевым ресурсом](https://www.rfc-editor.org/rfc/rfc9110#target.resource) и его текущей функциональностью.
- **Использование**:
  - Используется для удаления указанного ресурса сервера.

### [`CONNECT`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.6)

[`CONNECT`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.6) - СОЕДИНИТЬ

- **Команда серверу**: Установите туннель к серверу, идентифицированному целевым ресурсом.
- **Описание**: Метод `CONNECT` запрашивает, чтобы получатель установил туннель к серверу (**origin server**) назначения, определенному в цели запроса (**request**), и, в случае успеха, впоследствии ограничил свое поведение слепой пересылкой данных в обоих направлениях, пока туннель не будет закрыт.
- **Использование**:
  - Используется для переключения соединение в туннельный режим вместо получения содержимого (**content**). [Источник](https://www.rfc-editor.org/rfc/rfc9110#section-6.4.1-7)
- **Принимает**: заголовки

<details>
<summary>Обязательно использовать ":port" при создание цели запроса</summary>
<p>

`CONNECT` uses a special form of request target, unique to this method, consisting of only the host and port number of the tunnel destination, separated by a colon. There is no default port; a client MUST send the port number even if the `CONNECT` request is based on a URI reference that contains an authority component with an elided port ([Section 4.1](https://www.rfc-editor.org/rfc/rfc9110#uri.references)). For example,

`CONNECT` server.example.com:80 HTTP/1.1
Host: server.example.com

A server MUST reject a `CONNECT` request that targets an empty or invalid port number, typically by responding with a 400 (Bad Request) status code

</p>
</details>

### [`TRACE`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.8)

[`TRACE`](https://www.rfc-editor.org/rfc/rfc9110#section-9.3.8) - ОТСЛЕДИТЬ

- **Команда серверу**: Выполните проверку обратного цикла (loop-back test) передачи сообщений по пути к целевому ресурсу.
- **Описание**: Метод `TRACE` запрашивает удаленный обратный цикл (loop-back) сообщения запроса на уровне приложения.
- **Использование**:
  - Метод `TRACE` позволяет клиенту видеть, что он получает от другого конец цепочки запросов и использовать эти данные для тестирования или диагностики информация.
- **Принимает**: Принимает только заголовки (**headers**)
- **Возвращает**: Сервер **ДОЛЖЕН (SHOULD)** отразить (вернуть) полученное сообщение, исключая некоторые поля

[Все серверы должны поддерживать методы `GET` и `HEAD`. Остальные методы опциональные.](https://www.rfc-editor.org/rfc/rfc9110#section-9.1-9).

## Notes

Методы: `CONNECT`, `TRACE`, `TRACK` запрещены для использования в **Fetch API**. [Источник](https://fetch.spec.whatwg.org/#forbidden-method)

Список методов, которые разрешены целевым ресурсом, могут быть указаны в заголовке [`Allow`](https://www.rfc-editor.org/rfc/rfc9110#section-10.2.1). Сервер (*origin server*) получающий метод запроса, который не распознан или не реализован, **ДОЛЖЕН (SHOULD)** ответить 501 (Не реализован)

Реализация методов запроса лежит на сервере. То есть, сервер может не использовать все методы. Он может, к примеру, не использовать `PUT` или `PATCH`, а использовать только `POST` и отправлять необходимые статусы и ресурсы, в зависимости от переданного URI, заголовков и контента.

### [Example of passing `PUT` method within HTTP body 📂](./examples/example-post-as-put.md)

<!-- TODO: Разобраться как правильно и лучше называть поля сообщения - заголовок (header - так принято в **Fetch API**) или поле (field). Встретил так же такое: [Request header field](https://www.rfc-editor.org/rfc/rfc9110#name-request-context-fields). -->

[^1]: Полный список зарегистрированных методов запроса: <https://www.iana.org/assignments/http-methods/http-methods.xhtml>
[^2]: [It is not possible to issue HTTP request with OPTIONS * HTTP/1.1 start line in JavaScript - [*stackoverflow*]](https://stackoverflow.com/a/75835604/14615230)
[^3]: [**ISSUE** - How to send ‘OPTIONS * HTTP/1.1’ requests (asterisk form) with fetch()? - 📍 [*github*]](https://github.com/whatwg/fetch/issues/1622)
