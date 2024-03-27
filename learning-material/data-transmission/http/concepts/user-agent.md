# [User Agent](https://www.rfc-editor.org/rfc/rfc9110#name-user-agents)

**User Agent** - это любая клиентская программа, которая инициирует запрос.

- Примеры: Web Browsers, web crawlers (web-traversing robots), command-line инструменты, экраны рекламных щитов, бытовую технику, весы, лампочки, сценарии обновления встроенного ПО, мобильные приложения и устройства связи различных форм и размеров
- **Header**: [User-Agent](https://www.rfc-editor.org/rfc/rfc9110#name-user-agent)


## Header fields

### [User-Agent](https://www.rfc-editor.org/rfc/rfc9110#name-user-agent) - Агент Пользователя (Отправляется только агентом пользователя) 🎩
- **User-Agent** - Это поле содержит информацию об агенте пользователя (**user agent**), отправляющем запрос.
- **Состояние**: Поле состоит из одного или нескольких идентификаторов продукта, с опциональными комментариями, которые в совокупности идентифицируют программное обеспечение агента пользователя (**user agent**) и его важные субпродукты.
- **Использование**: Эту переданную информацию об агенте пользователя часто используют серверы для идентификации проблем совместимости с этим **user agent**, используют чтобы обойти или адаптировать ответы (**responses**), исходя из обнаруженных ограничений агента пользователя (**user agent**). Также используется для анализа использования браузера или операционной системы. **User agent** ДОЛЖЕН отправлять поле заголовка User-Agent в каждом запросе, если только специально не настроено не делать этого.
- **Дополнительно:** Похожее поле есть у ответа, только оно говорит о [Server](https://www.rfc-editor.org/rfc/rfc9110#name-server)

<details><summary>Примеры поля User-Agent</summary>
<p>

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36 Edg/122.0.0.0 - **Edge Browser**

User-Agent: curl/8.4.0 - **CURL**

User-Agent: HTTPie - **HTTPie**

User-Agent: PostmanRuntime/7.36.3 - **Postman**

User-Agent:
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Code/1.87.0 Chrome/118.0.5993.159 Electron/27.3.2 Safari/537.36 - **VSCode**

</p>
</details>
