# WebSocket

## Table of content

- [Overview](#overview)
  - [Frames](#frames)
    - [Frame types](#frame-types)
  - [WebSocket API](#websocket-api)
- [DevTools](#devtools)

## Overview

### Frames

В протоколе WebSocket данные передаются с использованием последовательности фреймов.

#### Frame types

- [**Control Frames**](https://www.rfc-editor.org/rfc/rfc6455#section-5.5) - Контролирующие фреймы
  - [**Close**](https://www.rfc-editor.org/rfc/rfc6455#section-5.5.1) - Отправляется с клиента/сервера для закрытия соединения. Должен иметь [статус код](https://www.rfc-editor.org/rfc/rfc6455#section-7.4). Может иметь [сообщение с причиной закрытия соединения](https://www.rfc-editor.org/rfc/rfc6455#section-7.1.6). Конечный адресат (endpoint) должен прислать в ответ тоже контролирующий фрейм ***Close***. OpCode = 8
  - [**Ping**](https://www.rfc-editor.org/rfc/rfc6455#section-5.5.2) - Отправляется с клиента/сервера для проверки жизнеспособности соединения. Конечный адресат (endpoint) должен вернуть контролирующий фрейм ***Pong***. OpCode = 9
  - [**Pong**](https://www.rfc-editor.org/rfc/rfc6455#section-5.5.3) - Отправляется в ответ на контролирующий фрейм ***Ping***. OpCode = 10
- [**Data Frames**](https://www.rfc-editor.org/rfc/rfc6455#section-5.6) - Фреймы данных
  - Текстовый фрейм (Текстовое сообщение) в формате UTF-8.  OpCode = 1
  - Бинарный фрейм (Бинарное сообщение). OpCode = 2

### WebSocket API

[WebSocket](https://websockets.spec.whatwg.org/#websocket) использует интерфейс [`MessageEvent`](https://html.spec.whatwg.org/multipage/comms.html#messageevent) для события [`message`](https://html.spec.whatwg.org/multipage/indices.html#event-message).

## DevTools

[Firefox DevTools](https://firefox-source-docs.mozilla.org/devtools-user/) лучше показывают внутреннее строение фреймов вебсокета (`OpCode`, `FinBit`, `MaskBit`).

В остальном лучше работает **Chrome DevTools**. Особенно в при изучении передачи бинарный фреймов - можно выбрать формат показа этих бинарный фреймов: `HEX`, `Base64`, `UTF-8`. Firefox же переводит сообщения сразу в UTF-8, что выглядит, как по мне не очень. (Не нашел возможность переключения)
