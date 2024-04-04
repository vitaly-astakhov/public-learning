**ECMAScript** — это объектно-ориентированный язык программирования для выполнения вычислений и управления вычислительными объектами в [хост-среде (*host environment*)](https://tc39.es/ecma262/multipage/overview.html#_ref_992).

**Хост-среда (*host environment*)** обычно включает в себя объекты или функции, которые позволяют получать входные данные (*input*) и предоставлять выходные данные (*output*) в качестве свойств глобального объекта [global object](https://tc39.es/ecma262/multipage/global-object.html#sec-global-object), определенных хостом ([host-defined](https://tc39.es/ecma262/multipage/overview.html#host-defined)).

**Хост-средой**, например, являются веб-браузеры, веб-серверы и их движки (например: [v8](https://v8.dev/), [Node.js](https://nodejs.org/en)).

___

### [Completion Record](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-completion-record-specification-type)

Тип спецификации **Completion Record**, который используется для объяснения распространения (*propagation*) значений и потока управления во время выполнения, например поведения операторов (`break`, `continue`, `return` и `throw`), которые выполняют нелокальную передачу управления.
