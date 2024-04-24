# Events

## Materials

- [Events [DOM spec]](https://dom.spec.whatwg.org/#events)
- [UI Events [W3C]](https://www.w3.org/TR/uievents)

## Table of content

- [Lists of event types](#lists-of-event-types)
- [Overview](#overview)
  - [Event](#event)
  - [Event targets](#event-targets)
    - [Event target](#event-target)
    - [Current event target](#current-event-target)
  - [Event listener](#event-listener)
  - [Event order](#event-order)
  - [Event type](#event-type)
  - [Event phase](#event-phase)
    - [Capture phase](#capture-phase)
    - [Target phase](#target-phase)
    - [Bubbling phase](#bubbling-phase)
  - [Propagation path](#propagation-path)
- [Event flow](#event-flow)
  - [Trusted](#trusted)
- [UI Events Interface Inheritance](#ui-events-interface-inheritance)
- [Event handlers](#event-handlers)
  - [Event handlers on elements, Document, and Window](#event-handlers-on-elements-document-and-window)

___

## Lists of event types

- [List of Event Types [UI Events spec]](https://www.w3.org/TR/uievents/#event-types-list)
- [Events [HTML spec]](https://html.spec.whatwg.org/multipage/indices.html#events-2)
- [Media Events [HTML spec]](https://html.spec.whatwg.org/multipage/media.html#mediaevents)
- [DND Events [HTML spec]](https://html.spec.whatwg.org/multipage/dnd.html#dndevents)

___

## Overview

### [Event](https://www.w3.org/TR/uievents/#event)

**Event** (событие) - это представление (*representation*) некоторого события (*occurrence*) (такого как щелчок мышью по представлению элемента, удаление дочернего узла из элемента или любое количество других возможностей), которое связано с его целью ([*event target*](https://www.w3.org/TR/uievents/#event-target)). Каждое событие является реализацией события определенного типа ([*event type*](https://www.w3.org/TR/uievents/#event-type)).

### Event targets

#### [Event target](https://www.w3.org/TR/uievents/#event-target)

**Event target** (цель события) - это объект, на который направлено событие (*event*), используя диспетчеризацию событий и поток событий DOM ([*Event dispatch and DOM event flow*](https://www.w3.org/TR/uievents/#event-flow)). Целью события является значение атрибута [`event.target`](https://dom.spec.whatwg.org/#dom-event-target).

#### [Current event target](https://www.w3.org/TR/uievents/#current-event-target)

**Current event target** (цель текущего события) - в потоке событий (*event flow*) целью текущего события (*current event target*) является объект, связанный с отправляемым в данный момент обработчиком события ([*event handler*](https://www.w3.org/TR/uievents/#event-handler)). Этот объект МОЖЕТ (MAY) быть самим объектом события ([*event target*](https://www.w3.org/TR/uievents/#event-target)) или одним из его предшественников (*ancestors*). Цель текущего события изменяется по мере распространения события ([*event*](https://www.w3.org/TR/uievents/#event)) от объекта к объекту на различных этапах ([*phases*](https://www.w3.org/TR/uievents/#phase)) потока событий. Целью текущего события является значение атрибута [`event.currentTarget`](https://dom.spec.whatwg.org/#dom-event-currenttarget).

### [Event listener](https://www.w3.org/TR/uievents/#event-listener)

**Event listener** (слушатель события) - объект, который реализует интерфейс [`EventListener`](https://dom.spec.whatwg.org/#callbackdef-eventlistener) и предоставляет метод обратного вызова [`handleEvent()`](https://dom.spec.whatwg.org/#dom-eventlistener-handleevent). Обработчики событий зависят от языка. Обработчики событий вызываются в контексте определенного объекта (текущего целевого объекта события ([*current event target*](https://www.w3.org/TR/uievents/#current-event-target))) и предоставляются вместе с самим объектом event.

По всей веб-платформе события передаются ([*dispatched*](https://dom.spec.whatwg.org/#concept-event-dispatch)) объектам, чтобы сигнализировать о возникновении событий, таких как сетевая активность или взаимодействие с пользователем. Эти объекты реализуют интерфейс [`EventTarget`](https://dom.spec.whatwg.org/#eventtarget)  и, следовательно, могут добавлять прослушиватели событий ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener)) для наблюдения за событиями, вызывая [`addEventListener()`](https://dom.spec.whatwg.org/#dom-eventtarget-addeventlistener).

Слушатели событий ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener) ) можно удалить, используя метод [`removeEventListener()`](https://dom.spec.whatwg.org/#dom-eventtarget-removeeventlistener)`, передающий те же аргументы.

В качестве альтернативы, слушатели событий ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener)) можно удалить, передав [`AbortSignal`](https://dom.spec.whatwg.org/#abortsignal) в опции [`addEventListener()`](https://dom.spec.whatwg.org/#dom-eventtarget-addeventlistener) и вызвав [`abort()`](https://dom.spec.whatwg.org/#dom-abortcontroller-abort) на контроллере, которому принадлежит сигнал.

### [Event order](https://www.w3.org/TR/uievents/#event-order)

**Event order** (порядок событий) - это последовательность (*sequence*), в которой происходят события из одного и того же источника событий или процесса с использованием одних и тех же или связанных интерфейсов событий. Например, в среде с мышью, сенсорной панелью и клавиатурой каждое из этих устройств ввода будет представлять собой отдельный источник событий, и каждое из них будет следовать своему порядку событий. Событие наведения курсора мыши на трекпад, за которым следует событие наведения курсора мыши ([`mousedown`](https://www.w3.org/TR/uievents/#mousedown)), не приведет к событию щелчка ([`click`](https://www.w3.org/TR/uievents/#click)).

> [!NOTE]
> Могут существовать взаимодействия между различными порядками событий. Например, событие [`click`](https://www.w3.org/TR/uievents/#click) может быть изменено одновременным нажатием клавиши ([`keydown`](https://www.w3.org/TR/uievents/#keydown)) (например, с помощью `Shift`+[`click`](https://www.w3.org/TR/uievents/#click)). Однако порядок событий (*event order*) в этих разных источниках событий будет разным.

### [Event type](https://www.w3.org/TR/uievents/#event-type)

**Event type** (тип события) - это объект [event](https://www.w3.org/TR/uievents/#event) с определенным именем, который определяет определенные условия запуска, свойства и другие характеристики, отличающие его от других типов событий. Например, тип события [`click`](https://www.w3.org/TR/uievents/#click) имеет другие характеристики, чем типы событий [`mouseover`](https://www.w3.org/TR/uievents/#mouseover) или [`load`](https://www.w3.org/TR/uievents/#load). Тип события отображается в качестве атрибута `[type](https://dom.spec.whatwg.org/#dom-event-type) в объекте event.

### [Event phase](https://www.w3.org/TR/uievents/#event-phase)

**Event phase** (фаза события) - это набор логических переходов от узла к узлу по дереву DOM, от [Window](https://www.w3.org/TR/uievents/#window) к объекту [`Document`](https://dom.spec.whatwg.org/#document), корневому элементу ([*root element*](https://www.w3.org/TR/uievents/#root-element)) и вниз к цели события (фаза захвата ([***capture phase***](https://www.w3.org/TR/uievents/#capture-phase))), к самой цели события (*event target*) (фаза цели ([***target phase***](https://www.w3.org/TR/uievents/#target-phase))) и обратно по той же цепочке (фаза всплытия ([***bubbling phase***](https://www.w3.org/TR/uievents/#bubble-phase))).

Узнать в какой фазе находится событие можно через аттрибут [`event.eventPhase`](https://dom.spec.whatwg.org/#dom-event-eventphase), который возвращает одно из чисел:

- `0` - для событий, которое в данный момент не отправлены
- `1` - для событий, которое в находятся в фазе захвата (*capture phase*)
- `2` - для событий, которое в находятся в фазе цели (*target phase*)
- `3` - для событий, которое в находятся в фазе всплытия (*bubbling phase*)

#### [Capture phase](https://www.w3.org/TR/uievents/#capture-phase)

**Capture phase** (фаза захвата) - это процесс, с помощью которого событие (*event*) может быть обработано одним из предков (*ancestors*) объекта *до того (**before**)*, как оно будет обработано объектом цели события ([*event target*](https://www.w3.org/TR/uievents/#event-target)). То есть, объект события распространяется через предков (*ancestors*) цели события от [Window](https://www.w3.org/TR/uievents/#window) к родительскому объекту (*target's parent*) цели события.

#### [Target phase](https://www.w3.org/TR/uievents/#target-phase)

**Target phase** (фаза цели) - это процесс, с помощью которого цель события ([*event target*](https://www.w3.org/TR/uievents/#event-target)) может обрабатывать событие (*event*). То есть, объект события достигает цели события ([*event target*](https://www.w3.org/TR/uievents/#event-target)). Эта фаза также известна как *фаза достижения цели (at-target phase)*. Если тип события ([*event type*](https://www.w3.org/TR/uievents/#event-type)) указывает на то, что событие не всплывает (*doesn't bubble*), то объект события остановится после завершения этой фазы.

#### [Bubbling phase](https://www.w3.org/TR/uievents/#bubble-phase)

**Bubbling phase** (фаза всплытия) - это процесс, с помощью которого событие (*event*) может быть обработано одним из предков (*ancestors*) объекта *после того (**after**)*, как оно будет обработано объектом цели события ([*event target*](https://www.w3.org/TR/uievents/#event-target)). То есть, объект события распространяется по предкам целевого объекта в обратном порядке, начиная с родительского объекта (*target's parent*) целевого объекта и заканчивая [Window](https://www.w3.org/TR/uievents/#window).

The event object propagates through the target's ancestors in reverse order, starting with the target's parent and ending with the [Window](https://www.w3.org/TR/uievents/#window). This phase is also known as the *bubbling phase*.

### [Propagation path](https://www.w3.org/TR/uievents/#propagation-path)

Упорядоченный набор целей текущего события ([*current event targets*](https://www.w3.org/TR/uievents/#current-event-target)), через которые объект события будет последовательно проходить на пути к цели события и обратно. По мере распространения (*propagation*) события каждая цель текущего события ([*current event target*](https://www.w3.org/TR/uievents/#current-event-target)) на пути распространения, в свою очередь, устанавливается как [`event.currentTarget`](https://dom.spec.whatwg.org/#dom-event-currenttarget). Путь распространения изначально состоит из одной или нескольких фаз события ([*event phases*](https://www.w3.org/TR/uievents/#event-phase)), определяемых типом события ([*event type*](https://www.w3.org/TR/uievents/#event-type)), но МОЖЕТ (MAY) прерываться. Также известный как цепочка целей события (*event target chain*).

___

## [Event flow](https://www.w3.org/TR/uievents/#event-flow)

Объекты события (event objects) отправляются адресату события ([*event target*](https://www.w3.org/TR/uievents/#event-target)). Но прежде чем начать отправку, необходимо сначала определить путь распространения ([*propagation path*](https://www.w3.org/TR/uievents/#propagation-path)) объекта события.

Путь распространения ([*propagation path*](https://www.w3.org/TR/uievents/#propagation-path)) представляет собой упорядоченный список текущих целей события ([*current event targets*](https://www.w3.org/TR/uievents/#current-event-target)), через которые проходит событие. Этот путь распространения отражает иерархическую древовидную структуру документа. Последний элемент в списке является целью события ([*event target*](https://www.w3.org/TR/uievents/#event-target)), а предыдущие элементы в списке называются предками (*target's ancestors*) объекта, а непосредственно предшествующий элемент является родительским объектом (*target's parent*).

Как только путь распространения ([*propagation path*](https://www.w3.org/TR/uievents/#propagation-path)) определен, объект события проходит через одну или несколько фаз события ([*event phases*](https://www.w3.org/TR/uievents/#event-phase)).

Существует три фазы события: фаза захвата ([*capture phase*](https://www.w3.org/TR/uievents/#capture-phase)), фаза цели ([*target phase*](https://www.w3.org/TR/uievents/#target-phase)) и фаза всплытия ([*bubble phase*](https://www.w3.org/TR/uievents/#bubble-phase)). Объекты события завершают эти фазы, как описано ниже. Фаза будет пропущена, если она не поддерживается или если распространение объекта события было остановлено. Например, если атрибуту [`event.bubbles`](https://dom.spec.whatwg.org/#dom-event-bubbles) присвоено значение `false`, фаза всплытия будет пропущена, а если перед отправкой была вызвана функция [`event.stopPropagation()`](https://dom.spec.whatwg.org/#dom-event-stoppropagation), то будут пропущены все фазы.

___

Для того чтобы отменить действие по умолчанию ([*default action*](https://www.w3.org/TR/uievents/#default-action)), которое, возможно, находится у текущего события можно вызвать метод [`event.preventDefault()`](https://dom.spec.whatwg.org/#dom-event-preventdefault)

Действия по умолчанию ([*Default actions*](https://www.w3.org/TR/uievents/#default-action)) обычно выполняются после завершения отправки события, но в исключительных случаях они также могут быть выполнены непосредственно перед отправкой события.

Когда событие отменяется, условные действия по умолчанию ([*default actions*](https://www.w3.org/TR/uievents/#default-action), связанные с этим событием, пропускаются. Является ли объект события отменяемым, указывается атрибутом [`event.cancelable`](https://dom.spec.whatwg.org/#dom-event-cancelable). Вызов функции [`event.preventDefault()`](https://dom.spec.whatwg.org/#dom-event-preventdefault) останавливает все связанные с объектом события действия по умолчанию. Атрибут [`event.defaultPrevented`](https://dom.spec.whatwg.org/#dom-event-defaultprevented) указывает, было ли событие уже отменено (например, предыдущим прослушивателем событий ([*event listener*](https://www.w3.org/TR/uievents/#event-listener))). Если приложение DOM само инициировало отправку, то возвращаемое значение метода dispatchEvent() указывает, был ли объект event отменен.

События могут отправляться как [синхронно, так и асинхронно.](https://www.w3.org/TR/uievents/#sync-async)

### Trusted

Событиям, генерируемым пользовательским агентом либо в результате взаимодействия с пользователем, либо в результате прямых изменений в DOM, пользовательский агент доверяет (*trust*) с привилегиями, которые не предоставляются событиям, генерируемым скриптом (*script*) через [`event.createEvent()`](https://dom.spec.whatwg.org/#dom-document-createevent) метод, измененный с помощью метода [`event.initEvent()`](https://dom.spec.whatwg.org/#dom-event-initevent) или отправленный с помощью метода [`event.dispatchEvent()`](https://dom.spec.whatwg.org/#dom-eventtarget-dispatchevent). Атрибут [`event.isTrusted`](https://dom.spec.whatwg.org/#dom-event-istrusted) для доверенных (*trusted*) событий имеет значение `true`, в то время как для ненадежных (*untrusted*) событий значение атрибута [`event.isTrusted`](https://dom.spec.whatwg.org/#dom-event-istrusted) равно `false`.

Большинство ненадежных (*untrusted*) событий не запускают действия по умолчанию, за исключением события  [`click`](https://www.w3.org/TR/uievents/#click). Это событие всегда запускает действие по умолчанию, даже если атрибут [`event.isTrusted`](https://dom.spec.whatwg.org/#dom-event-istrusted) имеет значение `false` (это поведение сохраняется для обеспечения обратной совместимости). Все остальные ненадежные события ведут себя так, как если бы для этого события был вызван метод [`event.preventDefault()`](https://dom.spec.whatwg.org/#dom-event-preventdefault).

___

## UI Events Interface Inheritance

![UI Events Interface Inheritance](../../assets/event-inheritance.svg)

Источник: <https://www.w3.org/TR/uievents/#figure-event-inheritance>

___

## [Event handlers](https://html.spec.whatwg.org/multipage/webappapis.html#event-handler-attributes)

Помимо слушателей событий (*event listeners*), которые регистрируются через DOM, мы также можем работать с событиями, используя обработчики событий ([*event handlers*](https://html.spec.whatwg.org/multipage/webappapis.html#event-handler-attributes)).

Обработчики событий можно устанавливать двумя способами:

- Напрямую через **атрибуты элемента** в HTML. Например: (`<button onclick="myFunction()">Press me</button>`)
- Программно через свойства элементов в DOM. Например: `element.onclick = myFunction`

В обоих случаях имя обработчика событий представляет собой строку, которая всегда начинается с “on”, за которой следует название события, для которого он предназначен.

В отличие от слушателей событий (*event listeners*), для одного элемента можно добавить **только один** обработчик события (*event handler*). Если вы установите несколько обработчиков для одного события, активным останется только последний.

В большинстве случаев объект, предоставляющий обработчик событий (*event handler*), совпадает с объектом, к которому добавлен соответствующий прослушиватель событий (*event listener*). Однако элементы [`<body>`](https://html.spec.whatwg.org/multipage/sections.html#the-body-element) и [`<frameset>`](https://html.spec.whatwg.org/multipage/obsolete.html#frameset) предоставляют несколько обработчиков событий (*event handlers*), которые воздействуют на объект [Window](https://html.spec.whatwg.org/multipage/nav-history-apis.html#window) элемента, если таковой существует.

### [Event handlers on elements, Document, and Window](https://html.spec.whatwg.org/multipage/webappapis.html#event-handlers-on-elements,-document-objects,-and-window-objects)
