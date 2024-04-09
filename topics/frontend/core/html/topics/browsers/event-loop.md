# Event Loops

## Materials

### Documentation

- [ ] [WHATWG - Event loops](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops)
- [ ] [The Node.js Event Loop](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick#what-is-the-event-loop)

### Articles

- [x] [JavaScript Visualized: Event Loop *(dev.to)*](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif) 👍
- [x] [Event Loop. Мифы и реальность](https://habr.com/ru/articles/789572/) 👍

___

## Event Loop

**Циклы событий (event loop)** используются пользовательскими агентами для координации событий (**events**), взаимодействия с пользователем (**user interaction**), сценариев (**scripts**), рендеринга, работы в сети и т.д

У каждого агента ([**agent** 📂](./agent.md)) есть связанный цикл событий (*event loop*), который уникален для этого агента.

Цикл событий (*event loop*) имеет одну или несколько очередей задач (**task queues**). Очередь задач (**task queue**) - это набор (*set*) задач.

> [!NOTE]
> Task queues are sets, not queues, because the event loop processing model grabs the first runnable task from the chosen queue, instead of dequeuing the first task.

## Task

**Задача** (*task*) — это структура, которая имеет:

- [**steps**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-task-steps) - Последовательность шагов, определяющих работу, которую необходимо выполнить в рамках задачи.
- [**source**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-task-source) - Один из источников задач ([*task source*](https://html.spec.whatwg.org/multipage/webappapis.html#task-source)), используемый для группировки и сериализации связанных задач. В поле **source** указано, что каждая задача поступает из определенного источника задач (**task source**). Для каждого цикла обработки событий (*event loop*) каждый источник задач (*task source*) должен быть связан с определенной очередью задач  (*task queue*).
- [**document**](https://html.spec.whatwg.org/multipage/webappapis.html#concept-task-document) - `Document`, связанный с задачей, или значение NULL для задач, которые не находятся в цикле событий окна ([*window event loop*](https://html.spec.whatwg.org/multipage/webappapis.html#window-event-loop)).
- [**script evaluation environment settings object set**](https://html.spec.whatwg.org/multipage/webappapis.html#script-evaluation-environment-settings-object-set)

Задачи используют алгоритмы, которые отвечают за такие работы, как:

- **events** -
- **parsing** -
- **callbacks** -
- **using a resource** -
- **reacting to dom manipulation** -

В каждом цикле событий (**event-loop**) есть выполняющаяся в данный момент задача (**currently running task**), которая является либо задачей (*task*), либо NULL. Изначально это NULL.

### Microtask

Каждый цикл событий  (**event-loop**) имеет очередь микрозадач (**microtasks**), которая представляет собой очередь микрозадач, изначально пустую.

> [!NOTE]
> The microtask queue is not a task queue.

**Микрозадача (microtask)** — это разговорный способ обозначения задачи (**task**), созданной с помощью алгоритма очереди микрозадач ([*queue a microtask*](https://html.spec.whatwg.org/multipage/webappapis.html#queue-a-microtask)).
