# Event Loop

## Documentation
- [ ] [WHATWG - Event loops](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops)
- [ ] [The Node.js Event Loop](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick#what-is-the-event-loop)

## Articles
- [ ] [JavaScript Visualized: Event Loop _(dev.to)_](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif)


___

**Event loop (Цикл событий)** - это часть [HTML спецификации](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops) и используется для координации событий (**events**), взаимодействия с пользователем (**user interaction**), сценариев (**scripts**), рендеринга, работы в сети и т. д.

Цикл событий имеет одну или несколько очередей задач (**task queues**).

**Очередь задач (task queue)** - это набор задач (**task**).

**Задача (task)** — это структура, которая имеет:
- **steps**
- **source**
- **document**
- **script evaluation environment settings object set**

В каждом цикле событий (**event-loop**) есть выполняющаяся в данный момент задача (**task**), которая имеет либо значение task, либо значение NULL. Изначально это NULL. Он используется для обработки повторного входа.

Каждый цикл событий  (**event-loop**) имеет очередь микрозадач (**microtasks**), которая представляет собой очередь микрозадач, изначально пустую.

**Микрозадача (microtask)** — это разговорный способ обозначения задачи (**task**), созданной с помощью алгоритма очереди микрозадач.
