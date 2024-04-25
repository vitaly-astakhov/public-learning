# Web workers

## Materials

- [Web workers [HTML spec]](https://html.spec.whatwg.org/multipage/workers.html#workers)
- [Service Workers [W3C spec]](https://w3c.github.io/ServiceWorker)

## Libraries

- [comlink](https://github.com/GoogleChromeLabs/comlink)

## Table of contents

- [Overview](#overview)
- [Dedicated workers](#dedicated-workers)
- [Shared workers](#shared-workers)
- [Service worker](#service-worker)

## Overview

Web Workers API используется для запуска сценариев в фоновом режиме независимо от любых сценариев пользовательского интерфейса.

Это позволяет создавать длительно работающие скрипты, которые не прерываются скриптами, реагирующими на клики или другие действия пользователя, и позволяет выполнять длительные задачи, не снижая адаптивности страницы.

Рабочие программы (*workers*) (так называются эти фоновые скрипты) имеют относительно большой вес и не предназначены для использования в большом количестве. Например, было бы неуместно запускать одну рабочую программу (*worker*) для каждого пикселя четырехмегапиксельного изображения.

Как правило, ожидается, что рабочие системы будут работать долго (*long-lived*), будут иметь высокую начальную производительность (*start-up performance cost*) и высокую стоимость памяти для каждого экземпляра (*per-instance memory cost*).

Каждая рабочая программа (*worker*) имеет глобальную область видимости, которая является его "внутренней частью", которая определяется интерфейсом [`WorkerGlobalScope`](https://html.spec.whatwg.org/multipage/workers.html#workerglobalscope). [`WorkerGlobalScope`](https://html.spec.whatwg.org/multipage/workers.html#workerglobalscope) служит базовым классом для определенных типов объектов глобальной области worker, включая [`DedicatedWorkerGlobalScope`](https://html.spec.whatwg.org/multipage/workers.html#dedicatedworkerglobalscope), [`SharedWorkerGlobalScope`](https://html.spec.whatwg.org/multipage/workers.html#sharedworkerglobalscope), и[`ServiceWorkerGlobalScope`](https://w3c.github.io/ServiceWorker/#serviceworkerglobalscope).

У рабочих программ (*worker*), таких как [dedicated worker agent](https://html.spec.whatwg.org/multipage/webappapis.html#dedicated-worker-agent), [shared worker agent](https://html.spec.whatwg.org/multipage/webappapis.html#shared-worker-agent), или [service worker agent](https://html.spec.whatwg.org/multipage/webappapis.html#service-worker-agent) есть цикл событий (*event loop*), который называется [worker event loop](https://html.spec.whatwg.org/multipage/webappapis.html#worker-event-loop-2) и в качестве задач в котором используются только события, обратные вызовы и сетевая активность. Эти worker event loop создаются с помощью алгоритма запуска рабочего процесса ([*run a worker*](https://html.spec.whatwg.org/multipage/workers.html#run-a-worker)).

## [Dedicated workers](https://html.spec.whatwg.org/multipage/workers.html#worker)

Выделенные рабочие программы (*dedicated worker*) после создания привязываются к своему создателю, но порты сообщений могут использоваться для связи выделенной рабочей программы (*dedicated worker*) с несколькими другими контекстами просмотра или рабочими программами (*dedicated worker*) .

Для создания рабочей программы (*worker*) требуется URL-адрес файла JavaScript. Конструктор [`Worker()`](https://html.spec.whatwg.org/multipage/workers.html#dom-worker) вызывается с URL-адресом этого файла в качестве единственного аргумента.

Выделенные рабочие программы (*dedicated workers*) используют объекты [`MessagePort`](https://html.spec.whatwg.org/multipage/web-messaging.html#messageport) за кулисами и, таким образом, поддерживают все те же функции, такие как отправка структурированных данных, передача двоичных данных и передача других портов.

> [!NOTE]
> У неявного (implicit) [`MessagePort`](https://html.spec.whatwg.org/multipage/web-messaging.html#messageport), используемого выделенными рабочими программами (*dedicated workers*), при создании неявно (*implicitly*) включена очередь сообщений на порт ([*port message queue*](https://html.spec.whatwg.org/multipage/web-messaging.html#port-message-queue)), поэтому в интерфейсе [`Worker`](https://html.spec.whatwg.org/multipage/workers.html#worker) нет эквивалента методу `start()` интерфейса [`MessagePort`](https://html.spec.whatwg.org/multipage/web-messaging.html#messageport).

## [Shared workers](https://html.spec.whatwg.org/multipage/workers.html#sharedworker)

Разделяемые рабочие программы (*shared workers*) имеют имена, и после создания любой скрипт, запущенный в том же источнике, может получить ссылку на эту рабочую программу (*worker*) и взаимодействовать с ним.

Разделяемые рабочие программы (*shared workers*) идентифицируются по URL-адресу скрипта, использованного для его создания, при необходимости с явным (*explicit*) именем. Имя позволяет запускать несколько экземпляров определенного общего рабочего объекта.

Разделяемые рабочие программы (*shared workers*) ограничены по источнику ([*origin*](https://html.spec.whatwg.org/multipage/browsers.html#concept-origin)). Два разных сайта, использующих одинаковые имена, не будут конфликтовать. Однако, если страница попытается использовать то же имя разделяемой рабочей программы (*shared worker name*), что и другая страница на том же сайте, но с другим URL-адресом скрипта, это приведет к сбою.

Создание разделяемые рабочие программы (*shared workers*)выполняется с помощью конструктора [`SharedWorker()`](https://html.spec.whatwg.org/multipage/workers.html#dom-sharedworker). Этот конструктор принимает URL-адрес скрипта для использования в качестве первого аргумента и имя рабочего элемента, если таковое имеется, в качестве второго аргумента.

Взаимодействие с разделяемыми рабочими программами (*shared workers*) осуществляется с помощью явных (*explicit*) объектов `[MessagePort](https://html.spec.whatwg.org/multipage/web-messaging.html#messageport)`. Объект, возвращаемый конструктором [`SharedWorker()`](https://html.spec.whatwg.org/multipage/workers.html#dom-sharedworker), содержит ссылку на порт в своем атрибуте port.

Внутри разделяемой рабочий программы (*shared worker*) новые клиенты worker-сервера объявляются с помощью события [`connect`](https://html.spec.whatwg.org/multipage/indices.html#event-workerglobalscope-connect). Порт для нового клиента задается атрибутом [`source`](https://html.spec.whatwg.org/multipage/comms.html#dom-messageevent-source) объекта event.

## [Service worker](https://w3c.github.io/ServiceWorker)

[Примеры использования `navigation.serviceWorker` 📂](./examples/example-server-send-event.md)
