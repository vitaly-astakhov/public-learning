# [Data types](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types)

**ECMAScript** выделяет несколько языковых типов данных:

- primitive data types (`Undefine`, `Null`, `Boolean`, `Number`, `BigInt`, `String`, `Symbol`),
- `Object`

## Primitive

- [`Undefined`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-undefined-type) - тип данных представляющий значение, используемое, когда переменной не было присвоено значение.
- [`Null`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-null-type) - тип данных представляющей собой намеренное отсутствие какого-либо значения объекта.
- [`Boolean`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-boolean-type) - тип данных, который представляет собой логическую сущность, имеющую два значения: `true` и `false`.
- [`String`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-string-type) - тип данных, который представляет собой конечную упорядоченную последовательность из нуля или более 16-разрядных целых чисел (*integer*) без знака (“элементов”). Имеет максимальную длину $2^{53} - 1$ элементов. Используется обычно для представления текстовых данных. Каждый элемент занимает определенную позицию в последовательности (*sequence*), которая индексируется целым неотрицательным числом (*non-negative integers*).
- **numeric**
  - [`Number`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-number-type) - тип данных, представляющий числовое значение с плавающей запятой двойной точности (*double-precision floating-point*), соответствующее стандарту [IEEE 754-2019](https://tc39.es/ecma262/multipage/bibliography.html#sec-bibliography). Тип данных `Number` может представлять не больше $18,437,736,874,454,810,627$ значений (то есть, $2^{64} - 2^{53} + 3$), исключая специальные значения **NaN**.
    - **safe-integer (безопасные целые числа)** - это числа до $9,007,199,254,740,990$ (то есть, $2^{53} - 2$), которые JavaScript может точно представить.
    - специальные значения: **NaN** (*Not-a-Number*) и **Infinity**.
  - [`BigInt`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-bigint-type) - тип данных, представляющий целые числовое значение (*integer*). У типа данных `BigInt` нет лимита по размеру значений, в отличии от типа данных `Number`.
- [`Symbol`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-ecmascript-language-types-symbol-type) - тип данных, представляющий набор всех значений, отличных от строки (*string*), которые можно использовать в качестве ключа свойства объекта. [Table: Well-known Symbols](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#table-well-known-symbols).

## [Object 📂](./object.md)
