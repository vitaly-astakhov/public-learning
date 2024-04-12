# Common

<!-- TODO: Разобраться, что делать с этим файлом -->

HTTP предоставляет единый интерфейс для взаимодействия с ресурсом (**resource**) - путем отправки сообщений (**messages**), которые манипулируют представлениями или передают их.

Каждое сообщение (**message**) является либо запросом (**request**), либо ответом (**response**). Клиент создает сообщения-запросы (**request messages**), которые сообщают о его намерениях, и направляет эти сообщения на идентифицированный исходный сервер. Сервер прослушивает запросы (**requests**), анализирует каждое полученное сообщение, интерпретирует семантику сообщения применительно к идентифицированному целевому ресурсу и отвечает (**response**) на этот запрос одним или несколькими ответными сообщениями. Клиент проверяет полученные ответы (**responses**), чтобы убедиться, были ли выполнены его намерения, и определяет, что делать дальше, основываясь на кодах статуса и полученном контенте.

[Источник](https://www.rfc-editor.org/rfc/rfc9110#name-core-semantics)

___

HTTP is a client/server protocol that operates over a reliable transport- or session-layer "connection".

An HTTP "client" is a program that establishes a connection to a server for the purpose of sending one or more HTTP requests. An HTTP "server" is a program that accepts connections in order to service HTTP requests by sending HTTP responses.

The terms client and server refer only to the roles that these programs perform for a particular connection. The same program might act as a client on some connections and a server on others.

[Источник](https://www.rfc-editor.org/rfc/rfc9110#name-connections-clients-and-ser)

## HTTP normalization

[HTTP протокол расширяет "нормализацию" для URI](https://www.rfc-editor.org/rfc/rfc9110#name-https-normalization-and-com)

Нормализация - это процесс приведение URI к подобаемому для него вида.

<!-- TODO: Дополнить и поправить текст про URI нормализацию -->

[При работе с HTTP протоколом в URI нельзя передавать userinfo (user:password), который является частью URI компонента](https://www.rfc-editor.org/rfc/rfc9110#section-4.2.4) [**authority**](https://www.rfc-editor.org/rfc/rfc3986#section-3.2)
