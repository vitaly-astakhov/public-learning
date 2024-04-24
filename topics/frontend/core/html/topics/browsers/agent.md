# Agent

Эта тема сильно связано с JavaScript. [Подробнее тут 📂](../../../../../languages/javascript/topics/env-and-exec-contexts.md#Agent).

___

[**Агент (agent)**](https://tc39.es/ecma262/#sec-agents) - это независимый от архитектуры идеализированный "поток", в котором выполняется код JavaScript. Такой код может включать в себя несколько глобальных областей ([*realms*](https://html.spec.whatwg.org/multipage/webappapis.html#concept-global-object-realm)), которые могут синхронно обращаться друг к другу (определяется кластером агентов (**agent cluster**)), и, следовательно, должен выполняться в одном потоке выполнения. Источник: [Integration with the JavaScript agent formalism [HTML]](https://html.spec.whatwg.org/multipage/webappapis.html#integration-with-the-javascript-agent-formalism)

Два объекта `Window`, имеющие один и тот же агент, не означают, что они могут напрямую обращаться ко всем объектам, созданным в областях друг друга. Они должны быть из одного исходного домена ([same origin-domain](https://html.spec.whatwg.org/multipage/browsers.html#same-origin-domain)).

В веб-платформах существуют следующие типы агентов:

- [similar-origin window agent](https://html.spec.whatwg.org/multipage/webappapis.html#similar-origin-window-agent) - Содержит различные объекты [Window](https://html.spec.whatwg.org/multipage/nav-history-apis.html#window), которые потенциально могут взаимодействовать друг с другом либо напрямую, либо с помощью [document.domain](https://html.spec.whatwg.org/multipage/browsers.html#dom-document-domain).
- [dedicated worker agent](https://html.spec.whatwg.org/multipage/webappapis.html#dedicated-worker-agent)
- [shared worker agent](https://html.spec.whatwg.org/multipage/webappapis.html#shared-worker-agent)
- [service worker agent](https://html.spec.whatwg.org/multipage/webappapis.html#service-worker-agent)
- [worklet agent](https://html.spec.whatwg.org/multipage/webappapis.html#worklet-agent)

## Agent Cluster

<!-- TODO: Разобраться с темой Agent Cluster (дочитать статьи) -->

### Materials

- [Origin-keyed agent clusters [HTML]](https://html.spec.whatwg.org/multipage/browsers.html#origin-keyed-agent-clusters)
- [Requesting performance isolation with the Origin-Agent-Cluster header](https://web.dev/articles/origin-agent-cluster)
- [chrome - Feature: Origin-keyed agent clusters](https://chromestatus.com/feature/5683766104162304)
- [github- Примеры](https://github.com/domenic/origin-agent-cluster-demo.dev)

___

Кластер агентов (**agent cluster**) - это максимальный набор агентов, которые могут взаимодействовать, работая с общей памятью.

Каждый агент принадлежит ровно к одному кластеру агентов.

Концептуально концепция кластера агентов (**agent cluster**) представляет собой независимую от архитектуры идеализированную "границу процесса" (*"process boundary"*), которая объединяет несколько "потоков" (**агентов**). Кластеры агентов, определенные ECMAScript спецификацией, как правило, являются более строгими, чем реальные границы процессов, реализованные в пользовательских агентах. Источник: [Integration with the JavaScript agent cluster formalism [HTML]](https://html.spec.whatwg.org/multipage/webappapis.html#integration-with-the-javascript-agent-cluster-formalism)

Ключ кластера агентов (**agent cluster key**) - это источник сайта ([site](https://html.spec.whatwg.org/multipage/browsers.html#site)) или [tuple origin](https://html.spec.whatwg.org/multipage/browsers.html#concept-origin-tuple). Без действий веб-разработчика по созданию кластеров агентов с исходным ключом ([*origin-keyed agent clusters*](https://html.spec.whatwg.org/multipage/browsers.html#origin-keyed-agent-clusters)) это будет просто сайт (*site*).

Эквивалентной формулировкой может быть то что, что ключ кластера агентов может быть схемой и хостом (*scheme and host*) или источником (*origin*).

Примеры того, когда агент находится или не находится [можно найти здесь](https://html.spec.whatwg.org/multipage/webappapis.html#:~:text=The%20following%20pairs%20of%20global%20objects%20,each%20other).

Проверяет принадлежит ли window к кластеру агентов ([*agent cluster*](https://tc39.es/ecma262/#sec-agent-clusters)) с исходным ключом (**origin-keyed**): это означает, что операционная система предоставила выделенные ресурсы (например, процесс операционной системы) источнику этого окна, которые не являются общими. с окнами другого происхождения.

## Fields

### [Origin-Agent-Cluster](https://html.spec.whatwg.org/multipage/browsers.html#origin-agent-cluster) 🎩⬅️

<details>
<summary>Объяснение от Chat GPT-4</summary>

Поле HTTP-заголовка `Origin-Agent-Cluster` используется для запроса размещения связанного документа в агентском кластере, ключом которого является происхождение. Это означает, что ресурсы операционной системы (например, процесс операционной системы), используемые для обработки документа, должны быть общими только с другими документами из того же происхождения.

Это поле предназначено для улучшения производительности, поскольку документ, требующий значительных ресурсов, будет менее склонен ухудшать производительность документов из других происхождений. Современные веб-браузеры имеют мультипроцессорную архитектуру, в которой страницы из разных происхождений могут выполняться в разных процессах операционной системы. Это важно для производительности, так как это означает, что ресурсоемкая страница не будет так сильно влиять на другие страницы, открытые пользователем2.

Однако следует помнить, что агентские кластеры, ключом которых является происхождение, не следует рассматривать как функцию безопасности: браузеры могут игнорировать запрос по разным причинам или реализовать его таким образом, который не обеспечивает защиту памяти (например, используя отдельные потоки вместо отдельных процессов)
</details>
