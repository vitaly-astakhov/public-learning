# [Promise](https://tc39.es/ecma262/multipage/control-abstraction-objects.html#sec-promise-objects)

**Promise** - это объект, который используется в качестве заполнителя для конечных результатов отложенного (и, возможно, асинхронного) вычисления.

Любой **Promise** находится в одном из трех взаимоисключающих состояний:

- **fulfilled** (выполнено) - Promise **p** выполняется, если **p.then(f, r)** немедленно поставит в очередь задание ([*Job*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#job)) для вызова функции **f**.
- **rejected** (отклонено) - Promise **p** отклоняется, если **p.then(f, r)** немедленно поставит в очередь задание ([*Job*](https://tc39.es/ecma262/multipage/executable-code-and-execution-contexts.html#job)) для вызова функции **r**.
- **pending** (отложен) - Promise остается отложенным, если он не выполнен (*fulfilled*) и не отклонен (*rejected*).

Promise считается установленным (***settled***), если он не отложен (*is not pending*), т.е. если он либо выполнен, либо отклонен.

Promise считается выполненным (***resolved***), если он установлен (*settled*) или если он был “зафиксировано” (*"locked in"*) в соответствии с состоянием другого promise. Попытка разрешить (***resolve***) или отклонить (***reject***) выполненный (*resolved*) promise не имеет эффекта. Promise считается невыполненным (***unresolved***), если он не выполнено (*not resolved*). Невыполненное promise всегда находится в состоянии ожидания. Выполненный (*resolved*) promise может быть отложенным (*pending*), выполненным (*fulfilled*) или отклоненным (*rejected*).
