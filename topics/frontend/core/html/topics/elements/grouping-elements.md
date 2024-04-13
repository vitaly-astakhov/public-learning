# Grouping content elements

### [`<p>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-p-element) - paragraph

Элемент **`<p>`** представляет собой абзац/параграф (*paragraph* [в значении HTML спецификации](https://html.spec.whatwg.org/multipage/dom.html#paragraph))

### [`<hr>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-hr-element) - horizontal rule

Элемент **`<hr>`** представляет собой тематический разрыв на уровне абзаца/параграфа (*paragraph* [в значении HTML спецификации](https://html.spec.whatwg.org/multipage/dom.html#paragraph))

### [`<pre>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-pre-element) - prefrormatted

Элемент **`<pre>`** представляет собой блок предварительно отформатированного (***pre**formatted*) текста, структура которого остается без форматирования.

Чтобы представить блок компьютерного кода, элемент **`<pre>`** может использоваться с элементом `<code>`; для представления блока компьютерного вывода элемент **`<pre>`** может использоваться с элементом `<samp>`. Аналогично, элемент `<kbd>` может использоваться внутри элемента **`<pre>`** для обозначения текста, который должен ввести пользователь.

### [`<blockquote>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-blockquote-element) 🏷️

Элемент **`<blockquote>`**представляет раздел, цитируемый (*quoted*) из другого источника.

## List elements

### [`<ol>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-ol-element) - ordered list 🏷️

Элемент **`<ol>`** представляет собой список (*list*) элементов, в котором элементы были намеренно упорядочены (*order*) таким образом, что изменение порядка изменило бы значение документа.

Атрибут [`reversed`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-reversed), если присутствует, изменяет порядок нумерования элементов, которые находятся внутри **`<ol>`**.

Атрибут [`start`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-start), если присутствует, определяет начальное число с которого начинается порядок для элементов, которые находятся внутри **`<ol>`**.

Атрибут [`type`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-type), если присутствует и соответствует одному из ключевых слов [представленных в таблице](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-ol-type), определяет типа маркера, который применяется для маркирования элементов, которые находятся внутри **`<ol>`**.

### [`<ul>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-ul-element) - unordered list

Элемент **`<ul>`** представляет собой список (*list*) элементов, порядок следования которых не важен, то есть изменение порядка не приведет к существенному изменению смысла документа, то есть элементы не упорядочены (*unordered*).

### [`<menu>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-menu-element)

Элемент **`<menu>`** представляет собой панель инструментов (*toolbar*), состоящую из ее содержимого в виде неупорядоченного списка элементов (представленных элементами `<li>`), каждый из которых представляет собой команду, которую пользователь может выполнить или активировать.

> [!NOTE]
> Элемент **`<menu>`** - это просто семантическая альтернатива элемента `<ul>` для выражения неупорядоченного (*unordered*) списка команд ("панель инструментов").

<!-- TODO: Поискать сайты, которые используют элемент menu

И добавить сюда как примеры
-->

### [`<li>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-li-element) - list item 🏷️

Элемент **`<li>`** представляет элемент списка (*list item*). Если его родительским элементом является элемент `<ol>`, `<ul>` или `<menu>`, то элемент является элементом списка родительского элемента, как определено для этих элементов.

Атрибут [`value`](https://html.spec.whatwg.org/multipage/grouping-content.html#attr-li-value), если он присутствует, должен быть допустимым целым числом. Он используется для определения порядкового значения ([*ordinal value*](https://html.spec.whatwg.org/multipage/grouping-content.html#ordinal-value)) элемента списка, если владельцем элементов списка **`<li>`** является элемент `<ol>`.

## Description elements

### [`<dl>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dl-element) - description list

Элемент **`<dl>`** представляет собой список ассоциаций, состоящий из нуля или более групп имен и значений, можно думать как о списке описаний (*description list*). Группа имя-значение (*name-value*) состоит из одного или нескольких имен (элементы `<dt>`, возможно, как дочерние элементы дочернего элемента `<div>`), за которыми следует одно или несколько значений (элементы `<dd>`, возможно, как дочерние элементы дочернего элемента `<div>`), игнорирующих любые узлы, кроме дочерних элементов `<dt>` и `<dd>`, и элементов `<dt>` и `<dd>` которые являются дочерними элементами элемента `<div>`. В пределах одного элемента **`<dl>`** для каждого имени не должно быть более одного элемента `<dt>`.

Группами "имя-значение" (*name-value*)  могут быть термины и определения, темы и значения метаданных, вопросы и ответы или любые другие группы данных "имя-значение".

Элемент **`<dl>`**  можно использовать для определения словарного запаса, как в словаре. [Пример](https://html.spec.whatwg.org/multipage/grouping-content.html#:~:text=A%20dl%20can%20be%20used%20to%20define%20a%20vocabulary%20list,%20like%20in%20a%20dictionary).

<details>
<summary>Примеры использования элемента dl</summary>

Источник: <https://developer.mozilla.org/en-US/docs/Web/HTML>

```html
<dl>
  <dt id="html_introduction"><a href="#html_introduction">HTML Introduction</a></dt>
  <dd>
    <p>If you're new to web development, be sure to read our <a href="/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics">HTML Basics</a> article to learn what HTML is and how to use it.</p>
  </dd>
  <dt id="html_tutorials"><a href="#html_tutorials">HTML Tutorials</a></dt>
  <dd>
    <p>For articles about how to use HTML, as well as tutorials and complete examples, check out our <a href="/en-US/docs/Learn/HTML">HTML Learning Area</a>.</p>
  </dd>
  <dt id="html_reference"><a href="#html_reference">HTML Reference</a></dt>
  <dd>
    <p>In our extensive <a href="/en-US/docs/Web/HTML/Reference">HTML reference</a> section, you'll find the details about every element and attribute in HTML.</p>
  </dd>
</dl>

```

</details>

### [`<dt>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dt-element) - description term

Элемент **`<dt>`** представляет термин, или название, часть группы описаний терминов в списке описаний (элемент `<dl>`).

### [`<dd>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dd-element) - description definition

Элемент **`<dd>`** представляет описание, определение (*definition*) или значение, часть группы терминов-описаний (*term-description*) в списке описаний (элемент `<dl>`).

## Figure elements

### [`<figure>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-figure-element)

Элемент **`<figure>`** представляет собой некоторый потоковый контент ([*flow content*)](https://html.spec.whatwg.org/multipage/dom.html#flow-content-2), необязательно с заголовком (*caption*), которое является самодостаточным ([*self-contained*](https://html.spec.whatwg.org/multipage/grouping-content.html#:~:text=in%20this%20context%20does%20not%20necessarily%20mean%20independent)) (например, полным предложением) и обычно упоминается как отдельная единица из основного потока (*main flow*) документа.

Элемент **`<figure>`** можно использовать для аннотирования иллюстраций, диаграмм, фотографий, списков кодов и т.д.

Первый дочерний элемент `<figcaption>` элемента, если таковой имеется, представляет заголовок содержимого элемента **`<figure>`**. Если нет дочернего элемента `<figcaption>`, то нет и подписи.

[Реальные примеры использования элемента figure 📂](./examples/example-figure.md)

### [`<figcaption>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-figcaption-element)

Элемент **`<figcaption>`** представляет собой заголовок или условные обозначения для остального содержимого родительского элемента **`<figcaption>`** `<figure>`, если таковой имеется.

### [`<main>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-main-element)

Элемент **`<main>`** представляет основное содержание документа.

В документе не должно быть более одного элемента **`<main>`**, для которого не указан атрибут [`hidden`.](https://html.spec.whatwg.org/multipage/interaction.html#attr-hidden)

### [`<search>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-search-element)

Элемент **`<search>`** представляет собой часть документа или приложения, содержащую набор элементов управления формой (*form controls*) или другое содержимое, связанное с выполнением операции поиска или фильтрации. Это может быть поиск по веб-сайту или приложению; способ поиска или фильтрации результатов поиска на текущей веб-странице; или глобальная функция поиска в Интернете.

### [`<div>` element](https://html.spec.whatwg.org/multipage/grouping-content.html#the-div-element) - division

Элемент **`<div>`** вообще не имеет особого значения. Он представляет своих дочерних элементов.

Элементы **`<div>`** могут быть полезны в стилистических целях или для оформления нескольких абзацев внутри раздела.

> [!NOTE]
> Авторам настоятельно рекомендуется использовать **`<div>`**-элемент в качестве последнего средства, когда другие элементы не подходят. Использование более подходящих элементов вместо **`<div>`**-элемента повышает доступность для читателей и упрощает обслуживание для авторов.
