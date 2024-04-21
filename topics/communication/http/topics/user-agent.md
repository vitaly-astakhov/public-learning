# User Agent

## Table of content

- [Overview](#overview)
- [Header fields](#header-fields)
  - [`User-Agent`](#user-agent-field)
- [HTML](#html)
  - [`Navigator`](#navigator)

## Overview

**Пользовательский агент (User Agent)** — это любой программный объект, который действует от имени пользователя, например, инициируя запрос, извлекая и отображая веб-контент и облегчая взаимодействие с ним конечного пользователя.

**Примеры пользовательских агентов:** Web Browsers, web crawlers (web-traversing robots), программы чтения с экрана (*screen readers*), command-line инструменты (например, [curl](https://curl.se/)), экраны рекламных щитов, бытовая техника, весы, лампочки, сценарии обновления встроенного ПО, мобильные приложения и устройства связи различных форм и размеров.

## Header fields

### [`User-Agent`](https://www.rfc-editor.org/rfc/rfc9110#name-user-agent) 🎩 🕵️ <a id="user-agent-field"></a>

- **`User-Agent`** (*пользовательский агент*) - Это поле содержит информацию об пользовательском агенте (***user agent***), который отправляет запрос на сервер.
- **Состояние**: Поле состоит из одного или нескольких идентификаторов продукта, с опциональными комментариями, которые в совокупности идентифицируют программное обеспечение пользовательского агента (**user agent**) и его важные субпродукты.
- **Использование**: Эту переданную информацию об агенте пользователя часто используют серверы для идентификации проблем совместимости с пользовательским агентом (*user agent*), это делают чтобы обойти или адаптировать ответы (*responses*), исходя из обнаруженных ограничений пользовательского агента (*user agent*). Также используется для анализа использования браузера или операционной системы. **User agent** **ДОЛЖЕН (SHOULD)** отправлять поле заголовка **`User-Agent`** в каждом запросе, если только специально не настроено не делать этого.
- **Дополнительно:** Похожее поле есть у ответа, только оно говорит о [Server](https://www.rfc-editor.org/rfc/rfc9110#name-server)

Значение поля **`User-Agent`** можно через аттрибут [`navigator.userAgent`](https://html.spec.whatwg.org/multipage/system-state.html#dom-navigator-useragent)

<details>
<summary>Примеры поля User-Agent</summary>
<p>

```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36 Edg/122.0.0.0 - **Edge Browser**
```

```
 User-Agent: curl/8.4.0 - **CURL**
```

```
User-Agent: HTTPie - **HTTPie**
```

```
User-Agent: PostmanRuntime/7.36.3 - **Postman**
```

```
User-Agent:
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Code/1.87.0 Chrome/118.0.5993.159 Electron/27.3.2 Safari/537.36 - **VSCode**

```

</p>
</details>

## HTML

### [`Navigator`](https://html.spec.whatwg.org/multipage/system-state.html#navigator)

Экземпляры (*instances*) [`Navigator`](https://html.spec.whatwg.org/multipage/system-state.html#navigator) представляют идентификатор и состояние пользовательского агента (клиента). Они также служат общим глобальным интерфейсом, в котором расположены различные API-интерфейсы, которые определены в HTML спецификации, а также других.
