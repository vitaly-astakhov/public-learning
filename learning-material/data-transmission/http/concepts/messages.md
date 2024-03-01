# Messages

Сообщение ([**message**](https://www.rfc-editor.org/rfc/rfc9110#section-6)) состоит из:
### [Control data](https://www.rfc-editor.org/rfc/rfc9110#section-6.2)
**Control data** - это описание и путь/направление сообщения. Описывает то, что получатель должен знать немедленно.
  - Для запросов (request) control data будет состоять из:  метода (method), цели запроса (request target), версии HTTP протокола.
  - Для ответов (response) control data будет состоять из: статуса (status code), опциональной фраза о причине, версии HTTP протокола
> [!Note]
> Существуют различия между тем как **control data** передается в сообщениях в зависимости от версии протокола

<details><summary>Подробнее</summary>
<p>

В HTTP/1.1 и более ранних протоколах **control data** отправляются в виде первой строки сообщения.
___
![Mozilla Firefox screenshot](https://github.com/vitaliiastakhov/learning-private/assets/68643256/aa989cac-d6b1-4204-bfed-d6591d8f502b)
В HTTP/2 и HTTP/3 **control data** передаются как _pseudo-header_ поля с зарезервированными именными префиксами (например, ":authority")
___
![HTTP/2 (Chrome DevTools screenshot)](https://github.com/vitaliiastakhov/learning-private/assets/68643256/50127998-7b22-4f8e-98fc-57f75fde2895)
![HTTP/2 Opened HAR file (Visual Studio Code screenshot)](https://github.com/vitaliiastakhov/learning-private/assets/68643256/e11103a7-0305-4a5b-85d1-ea70c6639096)

</p>
</details>

### [Headers fields](https://www.rfc-editor.org/rfc/rfc9110#section-6.3)
**Headers fields** используются для расширения **control data** и передачи дополнительной информации об отправителе, сообщении, содержимом или контексте. Описывает, что необходимо знать перед получением контента.
### [Content](https://www.rfc-editor.org/rfc/rfc9110#section-6.4)
**Content** - это контент/данные, который пересылают друг другу client и server . Контент может быть пустым, т.е. отсутствовать.
### [Trailers fields](https://www.rfc-editor.org/rfc/rfc9110#section-6.5)
- **Trailers fields** используются для передачи информации, полученной при отправке контента. Содержаться необязательные метаданные, которые были неизвестны до отправки содержимого
- **Trailers fields** могут быть полезны для предоставления проверки целостности сообщений, цифровых подписей, показателей доставки или информации о состоянии последующей обработки. [Источник](https://www.rfc-editor.org/rfc/rfc9110#section-6.5-1)
> [!Warning]
>TODO: Изучить для чего это может быть полезно



Сообщения с одинаковыми названиями должны не записываться в несколько строк поля с (будь то в заголовках (**header**) или трейлерах) или добавлять строку поля, когда строка поля с таким же именем уже существует в сообщении, так как порядок, в котором принимаются строки поля с одинаковым именем, имеет значение для интерпретации значения поля.

> [!Note]
> Но есть одно исключение: Set-Cookie

https://www.rfc-editor.org/rfc/rfc9110#section-5.3

Порядок, в котором строки полей с разными именами полей принимаются в не является существенным. Но cуществуют рекомендации.

> [!Warning]
> TODO: Найти рекомендации по порядку.

> [!Note]
> Firefox DevTools позволяет посмотреть порядок строк в HTTP сообщениях (есть toggle button, который называется "raw"), в свою очередь Chrome DevTools, такой фичей не обладают. (TODO: Проверить настройки Chrome DevTools, вдруг там есть такая опция)
