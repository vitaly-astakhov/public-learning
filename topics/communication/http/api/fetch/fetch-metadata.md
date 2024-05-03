# Fetch metadata

## Documentation

- [Fetch Metadata Request Headers](https://www.w3.org/TR/fetch-metadata/)

**Fetch Metadata Request Headers** - это набор полей, которые являются дополнительным контекстом об условиях из которого был сделан fetch запрос. Эти поля отправляются пользовательским агентом, и их можно использовать сервером для решений о предоставлении ресурса или его обработки.

Эти поля являются [forbidden request-header](https://fetch.spec.whatwg.org/#forbidden-request-header) и это значит, что их нельзя установить программно, например из JavaScript.

## Fields

### [Sec-Fetch-Dest](https://www.w3.org/TR/fetch-metadata/#sec-fetch-dest-header) 🎩➡️🕵️

**Sec-Fetch-Dest** - это поле указывает назначение запроса, определенные в [Fetch API](https://fetch.spec.whatwg.org/#concept-request-destination)

### [Sec-Fetch-Mode](https://www.w3.org/TR/fetch-metadata/#sec-fetch-mode-header) 🎩➡️🕵️

**Sec-Fetch-Mode** - это поле указывает режим запроса, определенные в [Fetch API](https://fetch.spec.whatwg.org/#concept-request-mode)

### [Sec-Fetch-Site](https://www.w3.org/TR/fetch-metadata/#sec-fetch-site-header) 🎩➡️🕵️

**Sec-Fetch-Site** - это поле указывает связь между источником инициатора запроса и источником его цели. Возможные значения для передачи: "cross-site", "same-origin", "same-site", и "none"

### [Sec-Fetch-User](https://www.w3.org/TR/fetch-metadata/#sec-fetch-user-header) 🎩➡️🕵️

**Sec-Fetch-User** - это поле указывает, был ли [навигационный запрос](https://fetch.spec.whatwg.org/#navigation-request) инициирован пользователем или нет. Это поле передается только для [навигационных запросов](https://fetch.spec.whatwg.org/#navigation-request) и только есть его значение равно `true`. Это поле передает только значение `?1`.

<!-- TODO: Разобраться почему передается значение "?1" вместо true в некоторых HTTP заголовках -->
