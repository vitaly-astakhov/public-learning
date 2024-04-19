# Hooks

**Hooks** (хуки) - это специальные функции, которые позволяют вашим компонентам использовать функции React.

## State hooks

### `useState`

### `useReducer`

Объект, который передается в dispatch (*отправка*), называется *action*.

> [!NOTE]
> Reducer named after the [reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce). The function you pass to `reduce` is known as a *"reducer"*. It takes the result so far and the current item, then it returns the next result. React reducers are an example of the same idea: they take the state so far and the action, and return the next state. In this way, they accumulate actions over time into state.
>
> Источник: <https://react.dev/learn/extracting-state-logic-into-a-reducer#why-are-reducers-called-this-way>

### [Comparing `useState` and `useReducer`](https://react.dev/learn/extracting-state-logic-into-a-reducer#comparing-usestate-and-usereducer)

## Ref

### useRef

Ref можно использовать, если вы хотите, чтобы компонент “запомнил” некоторую информацию, но не хотите, чтобы эта информация запускала новые рендеры ([*trigger new renders*](https://react.dev/learn/render-and-commit)).

Как и state, *refs* сохраняются React между повторными отображениями ( *re-renders*). Однако установка state повторно отображает (*re-render*) компонент. Изменение *ref* не приводит к повторному отображению компонента.

[How does useRef work inside?](https://react.dev/learn/referencing-values-with-refs)

Когда часть информации используется для рендеринга, сохраняйте ее в состоянии state. Когда часть информации нужна только обработчикам событий и ее изменение не требует повторного рендеринга, использование ref может быть более эффективным.

Объект ref имеет стабильную идентификацию (*stable identity*): React гарантирует, что [вы всегда будете получать один и тот же объект](https://react.dev/reference/react/useRef#returns) из одного и того же вызова `useRef` при каждом рендеринге.

[Возможное использование refs](https://react.dev/learn/referencing-values-with-refs#when-to-use-refs):

- Хранение идентификаторов тайм-аута ([*timeout IDs*](https://developer.mozilla.org/docs/Web/API/setTimeout))
- Хранение элементов DOM ([*DOM elements*](https://developer.mozilla.org/docs/Web/API/Element)) и управление ими
- Хранение других объектов, которые не являются необходимыми для вычисления JSX.

## Side effects hooks

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

## `useLayoutEffect`

**useLayoutEffect** - это версия хука **useEffect**, которая запускается перед тем, как браузер перерисует (*repaint*) экран.
