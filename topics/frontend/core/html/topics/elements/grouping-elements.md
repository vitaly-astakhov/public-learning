# Grouping content elements

### [`<p>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-p-element)

Элемент `<p>` представляет собой абзац/параграф (*paragraph* [в значении HTML спецификации](https://html.spec.whatwg.org/multipage/dom.html#paragraph))

### [`<hr>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-hr-element)

Элемент `<hr>` представляет собой тематический разрыв на уровне абзаца/параграфа (*paragraph* [в значении HTML спецификации](https://html.spec.whatwg.org/multipage/dom.html#paragraph))

### [`<pre>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-pre-element)

Элемент `<pre>` представляет собой блок предварительно отформатированного (***pre**formatted*) текста, структура которого остается без форматирования.

Чтобы представить блок компьютерного кода, элемент `<pre>` может использоваться с элементом `<code>`; для представления блока компьютерного вывода элемент `<pre>` может использоваться с элементом `<samp>`. Аналогично, элемент `<kbd>` может использоваться внутри элемента `<pre>` для обозначения текста, который должен ввести пользователь.

### [`<blockquote>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-blockquote-element) 🏷️

Элемент `<blockquote>` представляет раздел, цитируемый (*quoted*) из другого источника.

## List elements

### [`<ol>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-ol-element) 🏷️

Элемент `<ol>` представляет собой список (*list*) элементов, в котором элементы были намеренно упорядочены (*order*) таким образом, что изменение порядка изменило бы значение документа.

Атрибут [`reversed`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-reversed), если присутствует, изменяет порядок нумерования элементов, которые находятся внутри `<ol>`.

Атрибут [`start`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-start), если присутствует, определяет начальное число с которого начинается порядок для элементов, которые находятся внутри `<ol>`.

Атрибут [`type`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-type), если присутствует и соответствует одному из ключевых слов [представленных в таблице](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-type), определяет типа маркера, который применяется для маркирования элементов, которые находятся внутри `<ol>`.

### [`<ul>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-ul-element)

Элемент `<ul>` представляет собой список (*list*) элементов, порядок следования которых не важен, то есть изменение порядка не приведет к существенному изменению смысла документа, то есть элементы не упорядочены (*unordered*).

### [`<menu>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-menu-element)

Элемент `<menu>` представляет собой панель инструментов (*toolbar*), состоящую из ее содержимого в виде неупорядоченного списка элементов (представленных элементами `<li>`), каждый из которых представляет собой команду, которую пользователь может выполнить или активировать.

> [!NOTE]
> Элемент `<menu>` - это просто семантическая альтернатива элемента `<ul>` для выражения неупорядоченного (*unordered*) списка команд ("панель инструментов").

<!-- TODO: Поискать сайты, которые используют элемент menu

И добавить сюда как примеры
-->

### [`<li>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-li-element) 🏷️

Элемент `<li>` представляет элемент списка (*list item*). Если его родительским элементом является элемент `<ol>`, `<ul>` или `<menu>`, то элемент является элементом списка родительского элемента, как определено для этих элементов.

Атрибут [`value`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-li-value), если он присутствует, должен быть допустимым целым числом. Он используется для определения порядкового значения ([*ordinal value*](https://html.spec.whatwg.org/multipage/grouping-content.html#ordinal-value)) элемента списка, если владельцем элементов списка `<li>` является элемент `<ol>`.

## Description elements

### [`<dl>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dl-element)

### [`<dt>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dt-element)

### [`<dd>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dd-element)

### [`<figure>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-figure-element)

### [`<figcaption>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-figcaption-element)

### [`<main>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-main-element)

### [`<search>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-search-element)

### [`<div>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-div-element)
