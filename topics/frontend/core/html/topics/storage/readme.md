# Storage

## Materials

- [Storage Standard](https://storage.spec.whatwg.org)
- [Web storage [HTML spec]](https://html.spec.whatwg.org/multipage/webstorage.html#webstorage)
- [Cookie Store API](https://wicg.github.io/cookie-store/)

## Overview

Хранилище ([*storage endpoint*](https://storage.spec.whatwg.org/#storage-endpoint)) может быть либо локальным ([*local storage*](https://storage.spec.whatwg.org/#local-storage)) либо сессионным ([*session storage*](https://storage.spec.whatwg.org/#session-storage)).

Каждое хранилище ([*storage endpoint*](https://storage.spec.whatwg.org/#storage-endpoint)) имеет квоту ([*quota*](https://storage.spec.whatwg.org/#storage-bottle-quota)), которая равна нулю или числу, представляющему рекомендуемую квоту (в байтах) для каждой ячейки хранилища ([*storage bottle*](https://storage.spec.whatwg.org/#storage-bottle)), соответствующей хранилищу ([*storage endpoint*](https://storage.spec.whatwg.org/#storage-endpoint)).

Традиционно, когда у пользователя заканчивается место для хранения на устройстве, данные, сохраненные с помощью storage API, таких как `indexedDB`, `localStorage`, `sessionStorage` и [других](https://storage.spec.whatwg.org/#registered-storage-endpoints), теряются, и пользователь не может вмешаться. Однако постоянные корзины (*persistent buckets*) не могут быть удалены без согласия пользователя. Таким образом, это обеспечивает доступ к данным, которыми пользователи пользовались на собственных платформах, в Интернете.

Простой способ сделать хранилище постоянным - это вызвать метод [`persist()`](https://storage.spec.whatwg.org/#dom-storagemanager-persist). Он одновременно запрашивает разрешение у конечного пользователя и изменяет хранилище на постоянное после его предоставления.

Узнать является ли хранилище постоянным можно через [`navigator.storage.persisted()`](https://storage.spec.whatwg.org/#dom-storagemanager-persisted) или `navigator.permissions.query({ name: "persistent-storage" })`

> [!CAUTION]
> Странно, у меня на системе Windows 11 в браузерах на основе chromium (сам Chrome и Edge) метод [`persist()`](https://storage.spec.whatwg.org/#dom-storagemanager-persist) не вызывал окно permission для предоставления разрешения. А в Firefox все работало корректно.op

## [Web storage](https://html.spec.whatwg.org/multipage/webstorage.html#webstorage)

Каждый сайт имеет свою отдельную область хранения (*storage area*).

Оба интерфейса `localStorage` и `sessionStorage` наследуют интерфейс [`Storage`](https://html.spec.whatwg.org/multipage/webstorage.html#storage-2)

Оба интерфейса `localStorage` и `sessionStorage` [имеют одинаковую квоту на память](https://storage.spec.whatwg.org/#ref-for-storage-endpoint-quota), которая равна 5 MiB[^1].

Понять что `localStorage` и `sessionStorage` можно вызвав событие [`storage`](https://html.spec.whatwg.org/multipage/indices.html#event-storage). Событие `storage` имеет под собой интерфейс [StorageEvent](https://html.spec.whatwg.org/multipage/webstorage.html#storageevent)

[^1]: [Mebibyte](https://simple.wikipedia.org/wiki/Mebibyte)
