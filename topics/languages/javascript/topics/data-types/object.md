# Object

[`Object`](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#sec-object-type) - тип данных, который представляет собой набор свойств (*properties*), которые можно получить через ключевое значение (*key value*). Каждое свойство является либо свойством данных (*data property*), либо свойством доступа (*accessor property*).

Ключевым значением (*key value*) объекта могут быть следующие типы данных: `String`, `Symbol`.

## Properties

**Data property** - связывает ключевое значение (*key value*) со значением, которое является одним из типов данных, и набором логических атрибутов (например, `writable`, `enumerable`, `configurable`).

**Accessor property** - связывает ключевое значение (*key value*) с одной или двумя функциями доступа (*accessor function*) и набором логических атрибутов. Функции доступа используются для хранения или получения значений, связанного со свойством.

Таблица со всеми аттрибутами свойств объекта: [Attributes of an Object property](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#table-object-property-attributes)

Аттрибуты можно как получить используя метод глобального объекта [`Object.getOwnPropertyDescriptor`](https://tc39.es/ecma262/multipage/fundamental-objects.html#sec-object.getownpropertydescriptor), так и задать используя [`Object.defineProperty`](https://tc39.es/ecma262/multipage/fundamental-objects.html#sec-object.defineproperty)

## Function

Некоторые объекты являются вызываемыми (*callable object* [^1]) - это функции (*function*) или функциональные объекты ([function objects](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#function-object)). Все функции являются членами типа `Object`. Функция, связанная с объектом через свойство, называется методом (*method*).

Функции или функциональные объекты (*function object*) отличны от объектов, тем что имеют внутренний метод `[[Call]]`, который делает их вызываемыми.

**Constructor**  — это объект, который поддерживает внутренний метод `[[Construct]]`. Каждый объект, поддерживающий [[Construct]], должен поддерживать `[[Call]]`; то есть каждый конструктор должен быть функциональным объектом.

## Internal methods

Семантика объектов в ECMAScript определяется с помощью алгоритмов, называемых внутренними методами (*internal methods*). Каждый объект связан с набором (*list*) внутренних методов, которые определяют его поведение во время выполнения (*runtime behavior*).

Внутренние методы не являются частью языка ECMAScript, но при этом существуют методы в самом языке, которое имплементируют эти методы.

Таблица со всеми основными внутренними методами объекта: [Essential Internal Methods](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#table-essential-internal-methods)

<!-- TODO: Сделать таблицу сопоставления внутренних методов и как их можно вызывать в JavaScript -->

Внутренние методы и слоты в спецификации обозначаются в двойных квадратных скобках **[[ ]]**.

ECMAScript выделяет два вида объектов исходя из использования ими внутренних методов:

- **обычный объект (*ordinary object*)** - это объект, который удовлетворяет [критериям описанным в спецификации](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#ordinary-object).
- **экзотичный объект (*exotic object*)** - это объект, который не является обычным объектом (*ordinary object*)

Таблица с хорошо известными внутренними объектами: [Table: Well-Known Intrinsic Objects](https://tc39.es/ecma262/multipage/ecmascript-data-types-and-values.html#table-well-known-intrinsic-objects).

[^1]: <https://en.wikipedia.org/wiki/Callable_object>
