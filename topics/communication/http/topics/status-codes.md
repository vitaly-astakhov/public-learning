# [Status Codes](https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes)

Код состояния (**status code**) ответа - это трехзначный целочисленный (integer) код, который описывает результат запроса и семантику ответа, включая то, был ли запрос успешным и какое содержимое (**content**) вложено (если таковое имеется). Все действительные коды состояния находятся в диапазоне от 100 до 599 включительно.

Коды состояния имеют следующие категории:

- [1xx (Informational)](https://www.rfc-editor.org/rfc/rfc9110.html#status.1xx): запрос получен, обработка продолжается.
- [2xx (Successful)](https://www.rfc-editor.org/rfc/rfc9110.html#status.2xx): запрос был успешно получен, понят и принят.
- [3xx (Redirection)](https://www.rfc-editor.org/rfc/rfc9110.html#status.3xx): для завершения запроса необходимо предпринять дальнейшие действия.
- [4xx (Client Error)](https://www.rfc-editor.org/rfc/rfc9110.html#status.4xx): запрос содержит неверный синтаксис или не может быть выполнен.
- [5xx (Server Error)](https://www.rfc-editor.org/rfc/rfc9110.html#status.5xx): серверу не удалось выполнить очевидно действительный запрос.

Полный список зарегистрированных кодов статуса: <https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml>
