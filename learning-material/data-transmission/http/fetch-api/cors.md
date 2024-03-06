# Cross-Origin Resource Sharing (CORS)

Методы, которые считаются безопасными для **CORS**: `GET`, `HEAD`, or `POST`.


## Request

### [CORS-safelisted request header](https://fetch.spec.whatwg.org/#cors-safelisted-request-header)

Список полей заголовков, которые считаются безопасными при **CORS**. У этих полей есть ограничение, [подробнее тут](https://fetch.spec.whatwg.org/#cors-safelisted-request-header).

- [`Accept`](https://www.rfc-editor.org/rfc/rfc9110#section-12.5.1)
- [`Accept-Language`](https://www.rfc-editor.org/rfc/rfc9110#section-12.5.4)
- [`Content-Language`](https://www.rfc-editor.org/rfc/rfc9110#section-8.5)
- [`Content-Type`](https://www.rfc-editor.org/rfc/rfc9110#section-8.3)
- [`Range`](https://www.rfc-editor.org/rfc/rfc9110#section-14.2)

### [no-CORS-safelisted request-header name](https://fetch.spec.whatwg.org/#no-cors-safelisted-request-header-name)

- [`Accept`](https://www.rfc-editor.org/rfc/rfc9110#section-12.5.1)
- [`Accept-Language`](https://www.rfc-editor.org/rfc/rfc9110#section-12.5.4)
- [`Content-Language`](https://www.rfc-editor.org/rfc/rfc9110#section-8.5)
- [`Content-Type`](https://www.rfc-editor.org/rfc/rfc9110#section-8.3)

[forbidden request-header](https://fetch.spec.whatwg.org/#forbidden-request-header):

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


### Response

### [CORS-safelisted response-header name](https://fetch.spec.whatwg.org/#cors-safelisted-response-header-name)



- [`Cache-Control`](https://www.rfc-editor.org/rfc/rfc9111#name-cache-control)
- [`Content-Language`](https://www.rfc-editor.org/rfc/rfc9110#section-8.5)
- [`Content-Length`](https://www.rfc-editor.org/rfc/rfc9110#name-content-length)
- [`Content-Type`](https://www.rfc-editor.org/rfc/rfc9110#section-8.3)
- [`Expires`](https://www.rfc-editor.org/rfc/rfc9111#name-expires)
- [`Last-Modified`](https://www.rfc-editor.org/rfc/rfc9110.html#name-last-modified)
- [`Pragma`](https://www.rfc-editor.org/rfc/rfc9111#name-pragma)
- Любое другое поле, за исключением **forbidden response-header name**

[**forbidden response-header name**](https://fetch.spec.whatwg.org/#forbidden-response-header-name):
- "Set-Cookie"
- "Set-Cookie2"
