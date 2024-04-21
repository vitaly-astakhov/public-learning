# React

## Table of content

- [Component](#component)
  - [Key](#key)
- [State](#state)
  - [State batching](#state-batching)
  - [State hooks](#state-hooks)
    - [`useState`](#usestate)
    - [`useReducer`](#usereducer)
  - [Comparing `useState` and `useReducer`](#comparing-usestate-and-usereducer)
- [Refs](#refs)
  - [When to use refs](#when-to-use-refs)
  - [Ref hooks](#ref-hooks)
    - [`useRef`](#useref)
    - [`useImperativeHandle`](#useimperativehandle)
  - [Ref APIs](#ref-apis)
    - [`forwardRef`](#forwardref)
- [Side effects](#side-effects)
  - [`useEffect`](#useeffect)
  - [`useLayoutEffect`](#uselayouteffect)
  - [`useInsertionEffect`](#useinsertioneffect)
- [Performance](#performance)
  - [Performance hooks](#performance-hooks)
    - [`useMemo`](#usememo)
    - [`useCallback`](#usecallback)
    - [`useTransition`](#usetransition)
    - [`useDeferredValue`](#usedeferredvalue)

## Component

Каждый компонент React проходит один и тот же жизненный цикл:

- Компонент подключается (*mounts*) при добавлении на экран.
- Компонент обновляется (*updates*) при получении новых реквизитов или состояния, обычно в ответ на взаимодействие.
- Компонент отключается (*unmounts*) при удалении с экрана.

### Key

**Key** (ключ) - это специальное свойство (*property*), которое используется в React для идентификации компонентов, обычно, в массиве и оптимизации процесса их обновления.

**Key** может быть либо строкой либо числом.

Ключи используются в React, чтобы заставить React различать любые компоненты, чтобы проверять были компоненты изменены, добавлены или удалены.

По умолчанию React использует в качестве ключа порядок в родительском элементе для различения дочерних компонентов.

Из этого вытекает, что если мы добавляем или удаляем элементы из массива компонентов без указания уникальных ключей, React будет перерисовывать все компоненты начиная с измененного элемента.

## State

**State** является видом памяти, который хранится и управляется компонентом. Он используется для отслеживания информации, которая может изменяться со временем.

State фактически “живет” в самом React вне вашей функции компонента. Когда React вызывает компонент, он выдает вам снимок (*snapshot*) состояния для этого конкретного рендера. Компонент возвращает снимок (*snapshot*) пользовательского интерфейса со свежим набором props и обработчиков событий (*event handlers*) в своем JSX, все они рассчитаны с использованием значений состояния из этого рендера!

React сохраняет состояние компонента до тех пор, пока он отображается в своем положении в [дереве пользовательского интерфейса](https://react.dev/learn/understanding-your-ui-as-a-tree#the-render-tree), то есть, если компонент поменяет положение, или изменится его родительский элемент/компонент, или его заменит другой элемент, то состояние компонента не сохранится. Подробнее можно узнать тут: <https://react.dev/learn/preserving-and-resetting-state>

По умолчанию React сохраняет состояние компонента, пока он остается в том же положении, но это поведение можно изменить передав одинаковым компонентам, которые не меняют своей позиции, разные ключи в их свойства (*props*). Подробнее можно узнать тут: [пример 1](https://react.dev/reference/react/useState#resetting-state-with-a-key), [пример 2](https://react.dev/learn/preserving-and-resetting-state#resetting-a-form-with-a-key)

### State batching

React сохраняет значения состояния “фиксированными” в обработчиках событий одного рендера. Это означает, что внутри одного рендера (одной итерации цикла жизни компонента) значения состояния (*state*) не изменяются, даже если вызвать `setState` несколько раз в обработчике события (*event handler*).

React ожидает, пока не будет выполнен ***весь*** код в обработчиках событий, прежде чем обновлять состояние компонента, это называется [**batching**](https://react.dev/learn/queueing-a-series-of-state-updates#react-batches-state-updates).

Передача значений в функцию set (`setState`) создает очередь обновлений (*update queue*). Значение может либо заменять (**replace**) текущее значение состояния (*state*), которое находится в очереди (например, `setState(replacingState)`), либо добавлять следующее состояние, основанное на предыдущем состоянии в очереди, через функцию обновления (**updater function**) (например, `setState(prevState => prevState + newState)`).

Подробнее про **state batching** можно узнать тут: [Queueing a Series of State Updates](https://react.dev/learn/queueing-a-series-of-state-updates)

___

### State hooks

#### [`useState`](https://react.dev/reference/react/useState)

```JavaScript
const [state, setState] = useState(initialState)
```

**`useState`** - это React hook, который позволяет вам добавить переменную состояния в ваш компонент.

**`useState`** принимает как параметр начальное значение (`initialState`), который может быть любым типом данных. При этом если передается функция как `initialState`, она будет рассматриваться как инициализирующая функция (*initializer function*). Она должна быть чистой (*pure function*), не принимать аргументов и возвращать значение любого типа. React вызовет инициализирующую функцию (*initializer function*) при инициализации компонента и сохранит ее возвращаемое значение в качестве начального состояния.

[Примеры использования хука `useState` c инициализирующей функцией (*initializer function*) 📂](./examples/example-use-state.md#with-initializer-function)

`useState` возвращает tuple, в котором ровно два значения:

- Текущее состояние (*current state*), которое при первом отображении (*first render*) будет соответствовать переданному `initialState`.
- Функция set ([`set` function](https://react.dev/reference/react/useState#setstate)) - далее `setState`. Это функция, которая позволяет обновить состояние до другого значения и запустить повторный рендеринг.

`setState` принимает как параметр любое значение, которое может либо заменить (*replace*) текущее значение в состоянии компонента, либо, передавая функцию обновления (**updater function**), обновит состояние исходя из предыдущего значения. Подробнее можно прочитать в [секции State batching 📂](#state-batching).

> [!NOTE]
> React рекомендует относиться к объектам, в том числе и массивам, которые находятся в `useState`, как к неизменяемым. И передавать в `setState` *новый* объект или массив.
>
> Источник: <https://react.dev/learn/updating-arrays-in-state#updating-arrays-without-mutation>

> [!NOTE]
> Для работы с глубоко вложенными (*deeply nested*) объектами в состоянии, документация React предлагает использовать библиотеку [`use-immer`](https://github.com/immerjs/use-immer).
>
> Источник: <https://react.dev/learn/updating-objects-in-state#write-concise-update-logic-with-immer>

#### [`useReducer`](https://react.dev/reference/react/useReducer)

```JavaScript
const [state, dispatch] = useReducer(reducerFunc, initialArg, initFunc?)
```

**`useReducer`** - это React hook, который позволяет добавить reducer к вашему компоненту.

Объект, который передается в функцию [`dispatch`](https://react.dev/reference/react/useReducer#dispatch) (*отправка*), для обновления состояния компонента, называется действием (*action*), это обычно действие, выполняемое пользователем. Это может быть значение любого типа. По общему правилу (*by convention*), действие (*action*) обычно представляет собой объект со свойством `type`, идентифицирующим его, и, при необходимости, другими свойствами, содержащими дополнительную информацию.

Чтобы обновить состояние компонента используется функция `dispatch`, через которую React передает текущее состояние и действие (*action*) функции reducer, которая была установлена первым аргументом в hook **`useReducer`**.

[Примеры использования хука `useReducer` c инициализирующей функцией (*initializer function*) 📂](./examples/example-use-reducer.md)

> [!NOTE]
> Reducer, назван в честь JavaScript функции [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce). Функция, которая передается в функцию `reduce()`, называется ***reducer***. Она принимает *текущий результат* и *текущий элемент*, а затем возвращает *следующий результат*. Reducers в React являются примером той же идеи: они принимают *текущее состояние* и *действие (action)* и возвращают *следующее состояние*. Таким образом, они накапливают действия (*accumulate actions*) с течением времени в состоянии.
>
> Источник: <https://react.dev/learn/extracting-state-logic-into-a-reducer#why-are-reducers-called-this-way>

### [Comparing `useState` and `useReducer`](https://react.dev/learn/extracting-state-logic-into-a-reducer#comparing-usestate-and-usereducer)

___

## Refs

Ссылки (***refs***) в React позволяют компоненту хранить некоторую информацию, которая не используется для рендеринга. Использование refs целесообразно, когда необходимо, чтобы компонент “запомнил” некоторые данные, и при этом изменение этих данных не приводило к новым рендерам компонента ([*trigger new renders*](https://react.dev/learn/render-and-commit)).

Можно считать, что ссылка (*ref*) ссылается (*reference*) на объект в памяти компонента, аналогично тому, как JavaScript работает с объектами. Действительно, в React ***ref*** содержит в себе объект со свойством `current`, которому можно присвоить значение, передав его в хук `useRef`.

Как и состояние (*state*), ссылки (*refs*) сохраняются React между повторными отображениями (*re-renders*). Однако установка состояния (*state*) повторно перерисовывает (*re-render*) компонент. Изменение *ref* не приводит к повторному отображению компонента.

Объект ref имеет стабильную идентификацию (*stable identity*): React гарантирует, что [вы всегда будете получать один и тот же объект](https://react.dev/reference/react/useRef#returns) из одного и того же вызова `useRef` при каждом рендеринге.

Когда часть информации используется для рендеринга компонента, рекомендуется сохранять ее в состоянии (*state*) компонента. Когда часть информации нужна только обработчикам событий и ее изменение не требует повторного рендеринга компонента, использование ссылок (ref) может быть более эффективным.

[How does useRef work inside?](https://react.dev/learn/referencing-values-with-refs#how-does-use-ref-work-inside)

### [When to use refs](https://react.dev/learn/referencing-values-with-refs#when-to-use-refs)

- Хранение идентификаторов тайм-аута ([*timeout IDs*](https://developer.mozilla.org/docs/Web/API/setTimeout))
- Хранение элементов DOM ([*DOM elements*](https://developer.mozilla.org/docs/Web/API/Element)) и управление ими
- Хранение других объектов, которые не являются необходимыми для вычисления JSX.

### Ref hooks

#### [`useRef`](https://react.dev/reference/react/useRef)

**`useRef`** - это React hook, который позволяет ссылаться (*reference*) на значение, которое не нужно для рендеринга.

**`useRef`** возвращает объект ref *(ref object*) с единственным свойством `current`, для которого изначально было установлено указанное вами начальное значение (*initial value*).

При следующем отображении (*next render*) **`useRef`** вернет тот же объект и можно изменить его свойство `current`, чтобы сохранить информацию и прочитать ее позже.

#### [`useImperativeHandle`](https://react.dev/reference/react/useImperativeHandle)

**`useImperativeHandle`** — это хук в React, который позволяет дочернему компоненту предоставлять родительскому компоненту определенные функции или свойства посредством императивного (то есть, напрямого и управляемого) интерфейса.

**`useImperativeHandle`** hook используется только в сочетании [`forwardRef`](https://react.dev/reference/react/forwardRef)

[Примеры использования хука useImperativeHandle 📂](./examples/example-use-imperative-handle.md)

### Ref APIs

#### [`forwardRef`](https://react.dev/reference/react/forwardRef)

`forwardRef` позволяет компоненту предоставлять доступ к DOM-узлу родительскому компоненту с помощью ссылки (*ref*).

## Side effects

Эффекты (*effects*) позволяют указать побочные эффекты (*side effects*), которые вызываются самим рендерингом, а не конкретным событием.

Эффекты запускаются в конце коммита ([*commit*](https://react.dev/learn/render-and-commit)) после обновления экрана. В это время можно синхронизировать компоненты React с какой-либо внешней системой (например, сетью или сторонней библиотекой).

По умолчанию эффекты запускаются после каждого рендеринга, но можно указать React, чтобы он пропустил ненужный повторный запуск эффекта, указав массив зависимостей (*dependencies*) в качестве второго аргумента вызова useEffect.

React вызывает функцию очистки каждый раз перед повторным запуском эффекта

React вызывает функцию очистки (*cleanup function*) каждый раз перед повторным запуском эффекта и в последний раз, когда компонент будет размонтирован (*unmounts*) (удален).

> [!NOTE]
> Во время разработки React приложений можно столкнуться, делая debug через console.log() с неожиданным количеством выводов в консоль. Для React это правильное поведение при разработке. Повторно подключая (*remounting*) ваш компонент, React проверяет, что переход от одного компонента к другому не приведет к нарушению кода.
>
> Источник: <https://react.dev/learn/synchronizing-with-effects#step-3-add-cleanup-if-needed>, <https://react.dev/learn/synchronizing-with-effects#how-to-handle-the-effect-firing-twice-in-development>

> [!NOTE]
> В массив зависимостей можно не передавать объект ref, так как он имеет стабильную идентификацию (*stable identity*), то есть React гарантирует, что вы всегда будете получать один и тот же объект из одного и того же вызова useRef при каждом рендеринге. Также функции `set`, возвращаемые `useState`, также имеют стабильную идентификацию.
>
> Источник: <https://react.dev/learn/synchronizing-with-effects#why-was-the-ref-omitted-from-the-dependency-array>

### [`useEffect`](https://react.dev/reference/react/useEffect)

### [`useLayoutEffect`](https://react.dev/reference/react/useLayoutEffect)

**useLayoutEffect** - это версия хука **useEffect**, которая запускается перед тем, как браузер перерисует (*repaint*) экран.

### [`useInsertionEffect`](https://react.dev/reference/react/useInsertionEffect)

## Performance

### Performance hooks

#### [`useMemo`](https://react.dev/reference/react/useMemo)

#### [`useCallback`](https://react.dev/reference/react/useCallback)

#### [`useTransition`](https://react.dev/reference/react/useTransition)

#### [`useDeferredValue`](https://react.dev/reference/react/useDeferredValue)
