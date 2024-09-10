# Text (CSS)

## Overview

Основной единицей набора текста (*typesetting*) является символ/знак ([*character*](https://drafts.csswg.org/css-text-4/#character)), что такое символ/знак на самом деле, зависит от контекста, в котором используется этот термин.

Что касается верстки текста, то в качестве базовой единицы текста используется термин - типографская символическая единица ([*typographic character unit*](https://drafts.csswg.org/css-text-4/#typographic-character-unit)). Типографская символическая единица представляет собой единицу письменности, такую как буква латинского алфавита, слог Хангыль, китайский идеографический иероглиф, группа слогов Мьянмы, которая неотделима от конкретной типографской операции (разбивка на строки (*line-breaking*), эффект первой буквы (*first-letter effects*), отслеживание (*tracking*), выравнивание (*justification*), вертикальное расположение (*vertical arrangement*) и т.д.).

Типографская буквенная единица ([*typographic letter unit*](https://drafts.csswg.org/css-text-4/#typographic-letter-unit)) (или буква ([*letter*](https://drafts.csswg.org/css-text-4/#letter))) - это типографская символьная единица ([*typographic character unit*](https://drafts.csswg.org/css-text-4/#typographic-character-unit)), относящаяся к одной из общих категорий ([*general categories*](https://drafts.csswg.org/css-text-4/#unicode-general-category)) букв или цифр.

## Transforming Text

### [`text-transform`](https://drafts.csswg.org/css-text-4/#propdef-text-transform)

Свойство [**`text-transform`**](https://drafts.csswg.org/css-text-4/#propdef-text-transform) преобразует текст в целях стилизации. Оно не влияет на основное содержимое и не должно влиять на содержимое операции копирования и вставки обычного текста.

Нельзя полагаться на преобразование текста ([**`text-transform`**](https://drafts.csswg.org/css-text-4/#propdef-text-transform)) в семантических целях; скорее, правильная формулировка и семантика должны быть закодированы в тексте исходного документа и разметке.

Свойство [**`text-transform`**](https://drafts.csswg.org/css-text-4/#propdef-text-transform) может иметь следующие значения: [`none`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-none) | [[`capitalize`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-capitalize) | [`uppercase`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-uppercase) | [`lowercase`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-lowercase)] || [`full-width`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-full-width) || [`full-size-kana`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-full-size-kana) | [`math-auto`](https://drafts.csswg.org/css-text-4/#valdef-text-transform-math-auto).

### [`word-space-transform`](https://drafts.csswg.org/css-text-4/#propdef-word-space-transform)

Свойство [**`word-space-transform`**](https://drafts.csswg.org/css-text-4/#propdef-word-space-transform) изменяет визуализацию текста с применением альтернативных, для некоторых языков (в основном азиатских), способов разделения слов, либо с использованием разных разделительных символов, либо иногда вообще без видимых символов. Оно не влияет на основное содержимое и не должно влиять на содержимое операции копирования и вставки обычного текста.

Свойство [**`word-space-transform`**](https://drafts.csswg.org/css-text-4/#propdef-word-space-transform) может иметь следующие значения: [`none`](https://drafts.csswg.org/css-text-4/#valdef-word-space-transform-none) | [ [`space`](https://drafts.csswg.org/css-text-4/#valdef-word-space-transform-space) | [`ideographic-space`](https://drafts.csswg.org/css-text-4/#valdef-word-space-transform-ideographic-space) ] | [`auto-phrase`](https://drafts.csswg.org/css-text-4/#valdef-word-space-transform-auto-phrase).

## White space and text wrapping

К пробелам документа ([*document white space*](https://drafts.csswg.org/css-text-4/#white-space)) относятся пробелы ([*spaces*](https://drafts.csswg.org/css-text-4/#spaces)), табы ([*tabs*](https://drafts.csswg.org/css-text-4/#tabs)) и разрывы текстовых сегментов ([*segment break*](https://drafts.csswg.org/css-text-4/#segment-break)).

### [`white-space`](https://drafts.csswg.org/css-text-4/#propdef-white-space)

Свойство [**`white-space`**](https://drafts.csswg.org/css-text-4/#propdef-white-space) является сокращением (*shorthand*) для свойств [`white-space-collapse`](https://drafts.csswg.org/css-text-4/#propdef-white-space-collapse), [`text-wrap-mode`](https://drafts.csswg.org/css-text-4/#propdef-text-wrap-mode) и [`white-space-trim`](https://drafts.csswg.org/css-text-4/#propdef-white-space-trim).

### [`white-space-collapse`](https://drafts.csswg.org/css-text-4/#propdef-white-space-collapse)

Свойство [**`white-space-collapse`**](https://drafts.csswg.org/css-text-4/#propdef-white-space-collapse) отвечает за изменение визуализации/свертывания пробелов документов ([*white space*](https://drafts.csswg.org/css-text-4/#white-space)), к которым относятся пробелы, табы и разрывы текстовых сегментов ([*segment break*](https://drafts.csswg.org/css-text-4/#segment-break)). По умолчанию имеет значение [`collapsed`](https://drafts.csswg.org/css-text-4/#valdef-white-space-collapse-collapse), то есть последовательности пробелов сворачиваются (*collapse*) в один символ.

### [`white-space-trim`](https://drafts.csswg.org/css-text-4/#propdef-white-space-trim)

Свойство [**`white-space-trim`**](https://drafts.csswg.org/css-text-4/#propdef-white-space-trim) отвечает позволяет задавать порядок обрезания/срезания (*trim*) пробелов в начале и конце блока. По умолчанию имеет значение `none`, то если не происходит срезание пробелов.

Свойство [**`white-space-trim`**](https://drafts.csswg.org/css-text-4/#propdef-white-space-trim) имеет следующие возможные значения:

- `none`
- [`discard-before`](https://drafts.csswg.org/css-text-4/#valdef-white-space-trim-discard-before)
- [`discard-after`](https://drafts.csswg.org/css-text-4/#valdef-white-space-trim-discard-after)
- [`discard-inner`](https://drafts.csswg.org/css-text-4/#valdef-white-space-trim-discard-inner)
