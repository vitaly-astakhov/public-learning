# [Environment and execution contexts](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-executable-code-and-execution-contexts)

## [Environment Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#)

**Запись среды (Environment Record)** — это тип спецификации, используемый для определения связи (*binding*) идентификаторов с конкретными переменными и функциями на основе лексической структуры вложенности кода ECMAScript. Обычно запись среды связана с некоторой конкретной синтаксической структурой кода ECMAScript, такой как [FunctionDeclaration](https://tc39.es/ecma262/multipage/ecmascript-language-functions-and-classes.html#prod-FunctionDeclaration), [BlockStatement](https://tc39.es/ecma262/multipage/ecmascript-language-statements-and-declarations.html#prod-BlockStatement) или предложение [Catch](https://tc39.es/ecma262/multipage/ecmascript-language-statements-and-declarations.html#prod-Catch) [TryStatement](https://tc39.es/ecma262/multipage/ecmascript-language-statements-and-declarations.html#prod-TryStatement). Каждый раз, когда такой код вычисляется (*evaluation*), создается новая запись среды (**environment record**) для записи привязок идентификаторов, которые создаются этим кодом. Каждая запись среды (**environment record**) имеет поле `[[OuterEnv]]`, которое имеет либо значение NULL, либо ссылку на запись внешней среды (**outer environment record**).

**Environment Record** имеет свои подклассы: [Declarative Environment Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-declarative-environment-records), [Object Environment Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-object-environment-records), и [Global Environment Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-global-environment-records). [Function Environment Records](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-function-environment-records) и [Module Environment Records](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-module-environment-records) являются подклассами [Declarative Environment Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-declarative-environment-records)

**Environment Record** также отвечает за распознавание и операции, связанные со связкой (*binding*).
Environment Record определяет некоторые типы привязок по их изменяемости:

- неизменяемые (*immutable*) - не существуют для записей среды объекта ([*object environment*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-object-environment-records))
- изменяемые (*mutable*)

### Function Environment Record

Запись среды функции (**Function Environment Record**) - это запись среды,  которая используется для представления области верхнего уровня функции и обеспечивает привязку **this** и **super** исходя из объявлений функции. Наследует все методы [Declarative Environment Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-declarative-environment-records)

## [Realm](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-code-realms)

Область (**realm**) в спецификации ECMAScript это набор внутренних объектов (*intrinsic objects*), глобальной среды ECMAScript (*global environment*), всего кода ECMAScript, загружаемого в пределах этой глобальной среды (*global environment*), а также других связанных состояний и ресурсов, которым владеет агент (**agent**). Область (*realm*) представлена в виде [Realm Record](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#realm-record).

Область необходима, так как перед вычислением (*evaluation*) весь код ECMAScript должен быть связан с областью (*realm*).

## [Execution Contexts](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-execution-contexts)

<!-- TODO: Написать про execution contexts и execution context stack -->

## [Agent](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-agents)

Эта тема связана с темой из HTML спецификации, которую я [разбирал здесь 📂](../../../frontend/core/html/topics/browsers/agent.md).

___

Агент (**agent**) содержит набор контекстов выполнения ([execution contexts](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-execution-contexts)) ECMAScript, стек контекстов выполнения ([*execution context stack*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#execution-context-stack)), запущенный контекст выполнения ([*running execution context*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#running-execution-context)), запись агента ([*Agent Record*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#table-agent-record)) и исполняющий поток ([*executing thread*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#executing-thread)). Источник: [Agents [ECMAScript]](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-agents)

### [Agent Clusters](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#sec-agent-clusters)

Кластер агентов (**agent cluster**) - это максимальный набор агентов, которые могут взаимодействовать, работая с общей памятью.

Каждый агент принадлежит ровно к одному кластеру агентов.
