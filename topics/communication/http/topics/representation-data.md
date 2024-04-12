# [Representation Data](https://www.rfc-editor.org/rfc/rfc9110#section-8)

Отправитель (**client/server**), который генерирует сообщение (**message**), который содержит контент (**content**), **ДОЛЖЕН (SHOULD)** сгенерировать поле заголовка Content-Type в этом сообщении (**message**), если только предполагаемый тип носителя вложенного представления отправителю неизвестен. Источник: <https://www.rfc-editor.org/rfc/rfc9110#section-8.3-5>

На практике владельцы ресурсов не всегда должным образом настраивают свой **origin server** для предоставления правильного типа контента для данного представления (**representation**). Некоторые пользовательские агенты (**client agent**) проверяют контент и в определенных случаях переопределяют полученный тип (например, смотрите [Sniffing]).

Заголовки, которые определяют **representation data**:

- [Content-Type](https://www.rfc-editor.org/rfc/rfc9110#name-content-type)
  - При работе в HTML значение поля `Content-Type` можно получить через аттрибут документа `document.contentType`. Подробнее: [DOM spec](https://dom.spec.whatwg.org/#dom-document-contenttype).
- [Content-Encoding](https://www.rfc-editor.org/rfc/rfc9110#name-content-encoding)
- [Content-Language](https://www.rfc-editor.org/rfc/rfc9110#name-content-language) - Основная цель Content-Language - позволить пользователю идентифицировать и дифференцировать представления в соответствии с предпочтительным языком пользователя
- [Content-Length](https://www.rfc-editor.org/rfc/rfc9110#name-content-length)
- [Content-Location](https://www.rfc-editor.org/rfc/rfc9110#name-content-location)
  - Если URI в Content-Location не отличается от нами переданного URI.
    - Для изменяющих состояние запросов - **PUT** или **POST** - нахождение заголовка Content-Location подразумевает, что ответ сервера содержит новое представление этого ресурса, тем самым отличая его от представлений, которые могут сообщать только о действии (например, "Это сработало!"). Это позволяет разработчикам приложений обновлять свои локальные копии без необходимости последующего запроса GET.
    Источник: <https://www.rfc-editor.org/rfc/rfc9110#section-8.7-5>
- Возможное использование: [Указание на новый документ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Location#pointing_to_a_new_document_http_201_created)
