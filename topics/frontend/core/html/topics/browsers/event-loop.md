# Event Loops

## Materials

### Documentation

- [ ] [WHATWG - Event loops](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops)
- [ ] [The Node.js Event Loop](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick#what-is-the-event-loop)

### Articles

- [x] [JavaScript Visualized: Event Loop *(dev.to)*](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif) 👍
- [x] [Event Loop. Мифы и реальность](https://habr.com/ru/articles/789572/) 👍

## Table of content

- [Event Loop](#event-loop)
- [Task](#task)
  - [Microtask](#microtask)
- [Dialog methods task blocking behavior](#dialog-methods-task-blocking-behavior)

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

В каждом цикле событий (*event-loop*) есть выполняющаяся в данный момент задача (*currently running task*), которая является либо задачей (***task***), либо **NULL**. Изначально это **NULL**.

### Microtask

Каждый цикл событий (**event-loop**) имеет очередь микрозадач (**microtasks**), которая представляет собой очередь микрозадач, изначально пустую.

**Микрозадача (microtask)** — это разговорный способ обозначения задачи (**task**), созданной с помощью алгоритма очереди микрозадач ([*queue a microtask*](https://html.spec.whatwg.org/multipage/webappapis.html#queue-a-microtask)). Этот алгоритм используется в абстрактной операции [HostEnqueuePromiseJob](https://html.spec.whatwg.org/multipage/webappapis.html#hostenqueuepromisejob) которую содержит JavaScript, для планирования операций, связанных с Promise. HTML планирует (*schedule*) эти операции в очереди микрозадач (*microtask queue*).

Помимо неявного (*implicit*) добавления в очередь микрозадач, используя `Promise`, можно явно (*explicit*) установить задачу в эту очередь используя метод [`queueMicrotask(callback)`](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#dom-queuemicrotask).

Метод [`queueMicrotask(callback)`](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#dom-queuemicrotask) позволяет запланировать (*schedule*) обратный вызов (*callback*) в очереди микрозадач ([*microtask queue*](https://html.spec.whatwg.org/multipage/webappapis.html#microtask-queue)). Это позволяет запускать код этих задач, как только стек контекста выполнения JavaScript ([*JavaScript execution context stack*](https://tc39.es/ecma262/#execution-context-stack)) опустеет, что происходит после завершения выполнения всего синхронного JavaScript, выполняющегося в данный момент. Это не возвращает управление обратно в цикл обработки событий ([*event loop*](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop)), как это было бы в случае использования, например, [`setTimeout(f, 0)`](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#dom-settimeout).

> [!NOTE]
> Авторам следует знать, что планирование большого количества микрозадач снижает производительность так же, как и выполнение большого количества синхронного кода. И то, и другое не позволит браузеру выполнять свою собственную работу, например, рендеринг. Во многих случаях лучше использовать [`requestAnimationFrame()`](https://html.spec.whatwg.org/multipage/imagebitmap-and-animations.html#dom-animationframeprovider-requestanimationframe) или [`requestIdleCallback()`](https://w3c.github.io/requestidlecallback/#the-requestidlecallback-method). В частности, если целью является запуск кода перед следующим циклом рендеринга, то это и есть назначение [`requestAnimationFrame()`](https://html.spec.whatwg.org/multipage/imagebitmap-and-animations.html#dom-animationframeprovider-requestanimationframe).

[Примеры использования метода `queueMicrotask` 📂](./examples/example-queue-microtask.md)

## Dialog methods task blocking behavior

Логика, зависящая от [tasks](https://html.spec.whatwg.org/multipage/webappapis.html#concept-task) или [microtasks](https://html.spec.whatwg.org/multipage/webappapis.html#microtask), таких как загрузка [медиаданных](https://html.spec.whatwg.org/multipage/media.html#media-data) [мультимедийными элементами](https://html.spec.whatwg.org/multipage/media.html#media-element), приостанавливается при вызове [диалоговых методов](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#simple-dialogs), таких как: [`window.alert`](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#dom-alert),
[`window.confirm`](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#dom-confirm),
[`window.prompt`](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#dom-prompt).
