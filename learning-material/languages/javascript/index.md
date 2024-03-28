**ECMAScript** — это объектно-ориентированный язык программирования для выполнения вычислений и управления вычислительными объектами в [хост-среде (*host environment*)](https://tc39.es/ecma262/multipage/overview.html#_ref_992).

**Хост-среда (*host environment*)** обычно включает в себя объекты или функции, которые позволяют получать входные данные (*input*) и предоставлять выходные данные (*output*) в качестве свойств глобального объекта [global object](https://tc39.es/ecma262/multipage/global-object.html#sec-global-object), определенных хостом ([host-defined](https://tc39.es/ecma262/multipage/overview.html#host-defined)).

**Хост-средой**, например, являются веб-браузеры, веб-серверы и их движки (например: [v8](https://v8.dev/), [Node.js](https://nodejs.org/en)).

**ECMAScript** выделяет несколько типов данных:

- **primitive** - `Undefined`, `Null`, `Boolean`, `Number`, `BigInt`, `String`, `Symbol`
- **object** - `Object`

Функции являются вызываемым объектом (*callable object*)[^1]. Функция, связанная с объектом через свойство, называется методом.

Примитивное значение является членом одного из следующих встроенных типов: Undefine, Null, Boolean, Number, BigInt, String и Symbol; объект является членом встроенного типа Object; а функция является вызываемым объектом. Функция, связанная с объектом через свойство, называется методом.

[^1]: <https://en.wikipedia.org/wiki/Callable_object>
