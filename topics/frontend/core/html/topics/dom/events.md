# [Events](https://dom.spec.whatwg.org/#events)

По всей веб-платформе события передаются ([*dispatched*](https://dom.spec.whatwg.org/#concept-event-dispatch)) объектам, чтобы сигнализировать о возникновении событий, таких как сетевая активность или взаимодействие с пользователем. Эти объекты реализуют интерфейс [`EventTarget`](https://dom.spec.whatwg.org/#eventtarget)  и, следовательно, могут добавлять прослушиватели событий ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener)) для наблюдения за событиями, вызывая [`addEventListener()`](https://dom.spec.whatwg.org/#dom-eventtarget-addeventlistener)

Прослушиватели ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener) ) событий можно удалить, используя метод [`removeEventListener()`](https://dom.spec.whatwg.org/#dom-eventtarget-removeeventlistener)`, передающий те же аргументы.

В качестве альтернативы, прослушиватели событий ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener)) можно удалить, передав [`AbortSignal`](https://dom.spec.whatwg.org/#abortsignal) в [`addEventListener()`](https://dom.spec.whatwg.org/#dom-eventtarget-addeventlistener) и вызвав [`abort()`](https://dom.spec.whatwg.org/#dom-abortcontroller-abort) на контроллере, которому принадлежит сигнал.

## Interface [`Event`](https://dom.spec.whatwg.org/#event)

Объект **`Event`** называется просто событием (*event*). Он позволяет сигнализировать о том, что что-то произошло, например, о завершении загрузки изображения.

### Targets

У событий есть два вида целей (*targets*):

- [**target**](https://dom.spec.whatwg.org/#dom-event-target) - объект, к которому отправляется ([*dispatched*](https://dom.spec.whatwg.org/#concept-event-dispatch)) событие. (его цель ([*target*](https://dom.spec.whatwg.org/#event-target))).
- [**currentTarget**](https://dom.spec.whatwg.org/#dom-event-target) - объект, к которому привязан (*attached*) [event listener](https://dom.spec.whatwg.org/#concept-event-listener)'s [callback](https://dom.spec.whatwg.org/#event-listener-callback).

### [Event phases](https://dom.spec.whatwg.org/#dom-event-eventphase)

У событий есть 4 фазы событий (*event phases*).

- **NONE** (числовое значение 0) - события, которые в данный момент не отправлены, находятся в этой фазе.
- **CAPTURING_PHASE** (числовое значение 1) когда событие отправляется объекту, который участвует в DOM дереве ([tree](https://dom.spec.whatwg.org/#concept-tree)), оно будет находиться в этой фазе до того, как достигнет своей цели ([target](https://dom.spec.whatwg.org/#event-target)).
- **AT_TARGET** (числовое значение 2) - когда событие отправляется, оно находится в этой фазе на своей цели.
- **BUBBLING_PHASE** (числовое значение 3) - Когда событие отправляется объекту, участвующему в дереве, оно будет находиться в этой фазе после того, как достигнет своей цели.

Узнать в какой фазе находится событие можно через аттрибут [`event.eventPhase`](https://dom.spec.whatwg.org/#dom-event-eventphase)

Управлять фазами можно через методы:

- [`event.stopPropagation()`](https://dom.spec.whatwg.org/#dom-event-stoppropagation) - When [dispatched](https://dom.spec.whatwg.org/#concept-event-dispatch) in a [tree](https://dom.spec.whatwg.org/#concept-tree), invoking this method prevents *event* from reaching any objects other than the current object.
- [`event.stopImmediatePropagation()`](https://dom.spec.whatwg.org/#dom-event-stopimmediatepropagation) - Invoking this method prevents *event* from reaching any registered [event listeners](https://dom.spec.whatwg.org/#concept-event-listener) after the current one finishes running and, when [dispatched](https://dom.spec.whatwg.org/#concept-event-dispatch) in a [tree](https://dom.spec.whatwg.org/#concept-tree), also prevents *event* from reaching any other objects.

### Interface [`EventTarget`](https://dom.spec.whatwg.org/#eventtarget)

Объект **`EventTarget`** представляет собой цель, к которой может быть отправлено событие, когда что-то произошло.

С каждым объектом **`EventTarget`** связан список прослушивателей событий (список из нуля или более прослушивателей событий ([*event listeners*](https://dom.spec.whatwg.org/#concept-event-listener))). Изначально это пустой список.

Прослушиватель событий ([*event listener*](https://dom.spec.whatwg.org/#concept-event-listener)) может использоваться для наблюдения за конкретным событием и состоит из:

- **type** (a string)
- **callback** (null or an EventListener object)
- **capture** (a boolean, initially false)
- **passive** (null or a boolean, initially null)
- **once** (a boolean, initially false)
- **signal** (null or an AbortSignal object)
- **removed** (a boolean for bookkeeping purposes, initially false)
