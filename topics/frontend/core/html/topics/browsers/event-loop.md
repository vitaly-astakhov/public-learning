# Event Loop

## Documentation

- [ ] [WHATWG - Event loops](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops)
- [ ] [The Node.js Event Loop](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick#what-is-the-event-loop)

## Articles

- [x] [JavaScript Visualized: Event Loop *(dev.to)*](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif)

___

**Циклы событий (event loop)** используются пользовательскими агентами для координации событий (**events**), взаимодействия с пользователем (**user interaction**), сценариев (**scripts**), рендеринга, работы в сети и т.д

У каждого агента ([**agent** 📂](./agent.md)) есть связанный цикл событий (*event loop*), который уникален для этого агента.

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
