# Web Application Manifest

Иконка ⚠️ означает важные элементы, который важны для добавления в манифест приложения.

## Materials

### Documentation

- [W3C - Web Application Manifest](https://w3c.github.io/manifest)
- [W3C - Web App Manifest - Application Information](https://w3c.github.io/manifest-app-info/)
- [W3C - Manifest Incubations](https://wicg.github.io/manifest-incubations/#display_override-member)
- [`share_target` member](https://w3c.github.io/web-share-target/#share_target-member)

### Schemes

- <https://json.schemastore.org/web-manifest.json>
- <https://json.schemastore.org/web-manifest-combined.json>

## Table of content

- [Overview](#overview)
- [Manifest elements (members)](#manifest-elements-members)
  - [Localizable members](#localizable-members)
    - [`dir`](#dir)
    - [`lang`](#lang)
  - [Common member](#common-member)
    - [`name`](#name) ⚠️
    - [`short_name`](#short_name) ⚠️
    - [`scope`](#scope) ⚠️
    - [`icons`](#icons) [^1]
      - [Manifest image resources](#manifest-image-resources)
      - [`src`](#src)
      - [`sizes`](#sizes)
      - [`type`](#type)
      - [`label`](#label)
      - [`purpose`](#purpose)
        - [`monochrome`](#monochrome)
        - [`maskable`](#maskable)
        - [`any`](#any-default)
    - [`display`](#display)
    - [`orientation`](#orientation)
    - [`start_url`](#start_url) ⚠️
    - [`id`](#id) ⚠️
    - [`shortcuts`](#shortcuts)
  - [Color's members](#colors-members) [^1]
    - [`theme_color`](#theme_color)
    - [`background_color`](#background_color)
  - [External application resource members](#external-application-resource-members)
    - [`related_applications`](#related_applications)
    - [`prefer_related_applications`](#prefer_related_applications)
  - [Application information members](#application-information-members)
    - [`categories`](#categories)
    - [`description`](#description)
    - [`iarc_rating_id`](#iarc_rating_id)
    - [`screenshots`](#screenshots)
      - [`label`](#label-1)
      - [`platform`](#platform)
      - [`form_factor`](#form_factor)
- [Events](#events)

## Overview

Web Application Manifest - это файл на основе JSON, который предоставляет централизованное место для размещения метаданных, связанных с веб-приложением.

Используя эти метаданные, пользовательские агенты (*user agents*) могут предоставить разработчикам средства для создания пользовательского опыта, более сопоставимого с опытом работы в нативном приложении.

___

Манифест приложения ([**application manifest**](https://www.w3.org/TR/appmanifest/#dfn-manifest)) - это документ в формате JSON, содержащий параметры запуска и значения по умолчанию для веб-приложения при запуске.

Манифест может содержать в своем корне любой из следующих элементов, которые несут в себе мета информацию, определяющие приложение.

Для некоторых элементов манифеста приложения, можно в качестве запасного варианта для устаревших браузеров (*fallback for legacy browsers*) можно передать информацию через HTML элементы `<meta>` и `<link>`. [Пример](https://www.w3.org/TR/appmanifest/#using-a-link-element-to-link-to-a-manifest).

## Manifest elements (members)

### Localizable members

Локализируемыми элементами ([*localizable members*](https://www.w3.org/TR/appmanifest/#dfn-localizable-members)) - это элемент манифеста, который может быть локализован.

К локализуемым элементам относятся: [`name`](https://www.w3.org/TR/appmanifest/#dfn-name), [`short_name`](https://www.w3.org/TR/appmanifest/#dfn-short_name); под-элементы элемента [`shortcuts`](https://www.w3.org/TR/appmanifest/#shortcuts-member): [`name`](https://www.w3.org/TR/appmanifest/#dfn-name-0), [`short_name`](https://www.w3.org/TR/appmanifest/#dfn-short_name-0), [`description`](https://www.w3.org/TR/appmanifest/#dfn-description). Локализуемый элемент - это элемент манифеста, который может быть локализован.

В будущем, возможно, можно будет локализировать эти элементы через постфикс `_localized`: [Источник - **PR - 1101**](https://pr-preview.s3.amazonaws.com/w3c/manifest/pull/1101.html#x_localized-members).

```JSON

// Пример, возможной локализации элементов манифеста через постфикс `_localized`.

{
  "lang": "en-US",
  "name": "Color Picker",
  "name_localized": {
    "en-GB": "Colour Picker",
    "fr": "Sélecteur de Couleur"
  }
}

```

#### [`dir`](https://www.w3.org/TR/appmanifest/#dir-member)

Элемент[**`dir`**](https://www.w3.org/TR/appmanifest/#dir-member) определяет базовое направление для локализуемых элементов ([*localizable members*](https://www.w3.org/TR/appmanifest/#dfn-localizable-members)) манифеста. Значение элемента **`dir`** может быть задано как текстовое направление ([*text-direction*](https://www.w3.org/TR/appmanifest/#dfn-text-directions)).

#### [`lang`](https://www.w3.org/TR/appmanifest/#lang-member)

Элемент [**`lang`**](https://www.w3.org/TR/appmanifest/#lang-member) - это строка в виде языкового тега ([*language tag*](https://www.w3.org/TR/appmanifest/#dfn-language-tag)), который определяет язык для значений локализуемых элементов ([*localizable members*](https://www.w3.org/TR/appmanifest/#dfn-localizable-members)) манифеста.

Указание языка через элемент [**`lang`**](https://www.w3.org/TR/appmanifest/#lang-member) улучшает взаимодействие с пользователем, помогая пользовательским агентам (*user agent*) выбирать наиболее подходящие методы обработки или ресурсы, такие как шрифты, стиль оформления, расстановка переносов или преобразование текста в речь для обеспечения доступности.

### Common member

#### [`name`](https://www.w3.org/TR/appmanifest/#name-member)

Элемент [**`name`**](https://www.w3.org/TR/appmanifest/#name-member) - это строка, представляющая название веб-приложения в том виде, в каком оно обычно отображается пользователю (например, в списке других приложений или в качестве метки для значка).

Элемент [**`name`**](https://www.w3.org/TR/appmanifest/#dfn-name) служит доступным именем ([accessible name](https://www.w3.org/TR/accname-1.2/#dfn-accessible-name)) установленного веб-приложения ([*installed web application*](https://www.w3.org/TR/appmanifest/#dfn-installed-web-application)).

#### [`short_name`](https://www.w3.org/TR/appmanifest/#short_name-member)

Элемент [**`short_name`**](https://www.w3.org/TR/appmanifest/#short_name-member) - это строка, представляющая собой сокращенную версию названия веб-приложения. Он предназначен для использования в тех случаях, когда недостаточно места для отображения полного имени веб-приложения, которое определяется элементом [`name`](https://www.w3.org/TR/appmanifest/#name-member).

#### [`scope`](https://www.w3.org/TR/appmanifest/#dfn-scope)

Элемент [**`scope`**](https://www.w3.org/TR/appmanifest/#dfn-scope) сообщает браузеру, какие документы являются частью веб-приложения, а какие нет, и, следовательно, к какому набору веб-страниц "применяется" ([*applied*](https://www.w3.org/TR/appmanifest/#dfn-applied)) манифест, когда пользователь перемещается по веб-сайту.

Поддерживается только один путь к области видимости (*scope*).

```JSON
"scope": "/app/"
OR
"scope": "https://example.com/"
OR
"scope": "https://example.com/subdirectory/"
```

> [!NOTE]
> "Область действия по умолчанию" (*default scope*) (когда [**`scope`**](https://www.w3.org/TR/appmanifest/#dfn-scope) отсутствует, пуст или произошел сбой) - это начальный URL-адрес ([*start URL*](https://www.w3.org/TR/appmanifest/#dfn-start-url)), но с удаленными именем файла, запросом и фрагментом.

#### [`icons`](https://www.w3.org/TR/appmanifest/#icons-member)

Элемент [`icons`](https://www.w3.org/TR/appmanifest/#icons-member) [^1] - это изображения, которые служат в качестве символических представлений (*iconic representations*) веб-приложения в различных контекстах. Например, они могут использоваться для представления веб-приложения среди списка других приложений или для интеграции веб-приложения с переключателем задач операционной системы и/или системными настройками.

При построении элемента `icons` используются manifest image resource элементы.

##### [Manifest image resources](https://w3c.github.io/manifest/#manifest-image-resources)

Каждый ресурс изображения манифеста (*manifest image resource*) - это ресурс изображения ([*image resource*](https://www.w3.org/TR/image-resource/#dfn-image-resource)), который концептуально является частью веб-приложения и подходит для использования в различных контекстах в зависимости от семантики элемента, который использует объект (например, icon, который является частью меню приложения, и т.д.).

Ресурс изображения манифеста ([manifest image resource](https://w3c.github.io/manifest/#dfn-manifest-image-resource)) расширяет элементы ресурса изображения ([image resource](https://www.w3.org/TR/image-resource/#dfn-image-resource)) дополнительным элементом `purpose`.

Агенты пользователей **МОГУТ (MAY)** изменять изображения, связанные с ресурсом изображений manifest, чтобы они лучше соответствовали визуальному стилю платформы, прежде чем показывать их пользователю, например, закругляя углы или окрашивая их в определенный цвет. Разработчикам рекомендуется подготовить свои графические ресурсы к таким сценариям, чтобы избежать потери важной информации, например, из-за изменения цвета или обрезанных углов.

##### [`src`](https://www.w3.org/TR/image-resource/#src-member)

Элемент [**`src`**](https://www.w3.org/TR/image-resource/#src-member) - это URL-адрес, с которого пользовательский агент может извлекать данные изображения.

##### [`sizes`](https://www.w3.org/TR/image-resource/#dom-imageresource-sizes)

Элемент [**`sizes`**](https://www.w3.org/TR/image-resource/#dom-imageresource-sizes) эквивалентен атрибуту sizes элемента link и обрабатывается таким же образом.

Если доступно несколько словарей ресурсов изображений ([*`ImageResource`*](https://www.w3.org/TR/image-resource/#dom-imageresource) *dictionaries*), пользовательский агент **МОЖЕТ (MAY)** использовать значение [**`sizes`**](https://www.w3.org/TR/image-resource/#dom-imageresource-sizes), чтобы решить, какое изображение наиболее подходит для контекста отображения (и игнорировать любое неподходящее).

##### [`type`](https://www.w3.org/TR/image-resource/#dom-imageresource-type)

Элемент [**`type`**](https://www.w3.org/TR/image-resource/#dom-imageresource-type) представляет собой MIME-тип изображения ([*image MIME Type*](https://mimesniff.spec.whatwg.org/#image-mime-type)) для графического ресурса. Пользовательский агент **МОЖЕТ (MAY)** игнорировать типы мультимедиа, которые он не поддерживает.

Для графического ресурса ([*`ImageResource`*](https://www.w3.org/TR/image-resource/#dom-imageresource)) не существует [MIME type](https://mimesniff.spec.whatwg.org/#mime-type) по умолчанию. Элемент [`type`](https://www.w3.org/TR/image-resource/#dom-imageresource-type) является чисто рекомендательным. Агенты пользователей **ДОЛЖНЫ (MUST)** использовать правила поиска изображений специально ([*rules for sniffing images specifically*](https://mimesniff.spec.whatwg.org/#rules-for-sniffing-images-specifically)) для определения вычисляемого MIME-типа графического ресурса.

##### [`label`](https://www.w3.org/TR/image-resource/#label-member)

##### [`purpose`](https://www.w3.org/TR/appmanifest/#purpose-member)

Элемент [**`purpose`**](https://www.w3.org/TR/appmanifest/#purpose-member) представляет собой неупорядоченный набор уникальных маркеров, разделенных пробелом. Допустимые значения - это [icon purposes](https://w3c.github.io/manifest/#dfn-icon-purposes).

Когда ресурс с изображением манифеста используется в качестве значка, разработчик может намекнуть, что изображение предназначено для какой-то особой цели в контексте основной операционной системы (например, для лучшей интеграции). Пользовательские агенты **НЕ ДОЛЖНЫ (SHOULD NOT)** использовать значок иначе, чем для его заявленного в [icon purpose](https://w3c.github.io/manifest/#dfn-icon-purposes).

Существуют следующие назначения иконок (*icon purpose*):

###### [`monochrome`](https://w3c.github.io/manifest/#dfn-monochrome)

Пользовательский агент может отображать этот иконку там, где требуется монохромный значок со сплошной заливкой ([*monochrome icon with a solid fill*](https://w3c.github.io/manifest/#monochrome-icons-and-solid-fills)). Информация о цвете на иконке удаляется и используются только альфа-данные. Затем пользовательский агент может использовать этот значок как маску поверх любой сплошной заливки.
маскируемый

###### [`maskable`](https://w3c.github.io/manifest/#dfn-maskable)

Изображение разработано с учетом масок значков и безопасной зоны ([*icon masks and safe zone*](https://w3c.github.io/manifest/#icon-masks)), так что любая часть изображения, находящаяся за пределами безопасной зоны, может быть безопасно проигнорирована ([*safe zone*](https://w3c.github.io/manifest/#dfn-safe-zone)) и замаскирована агентом пользователя.

###### [`any`](https://w3c.github.io/manifest/#dfn-any) (**default**)

Пользовательский агент может свободно отображать иконку там, где не требуется "назначение" ([**`purpose`**](https://w3c.github.io/manifest/#dfn-purpose)). Например, графический ресурс манифеста с [`any`](https://w3c.github.io/manifest/#dfn-any) назначением не будет использоваться в контексте, где требуется ["monochrome"](https://w3c.github.io/manifest/#dfn-monochrome).

#### [`display`](https://www.w3.org/TR/appmanifest/#display-member)

Элемент [`display`](https://www.w3.org/TR/appmanifest/#display-member)  представляет собой предпочтительный режим отображения ([*display mode*](https://www.w3.org/TR/appmanifest/#dfn-display-mode)) веб-приложения разработчиком.

Режим отображения ([*display mode*](https://www.w3.org/TR/appmanifest/#dfn-display-mode)) представляет собой то, как веб-приложение представлено в контексте операционной системы.

Режим отображения ([*display mode*](https://www.w3.org/TR/appmanifest/#dfn-display-mode)) может быть одним из следующих:

- [`browser`](https://www.w3.org/TR/appmanifest/#dfn-browser) (**default**) - Открывает веб-приложение, используя специфичное для платформы соглашение об открытии гиперссылок в пользовательском агенте (например, на вкладке браузера или в новом окне).
- [`minimal-ui`](https://www.w3.org/TR/appmanifest/#dfn-minimal-ui) - Этот режим похож на [`standalone`](https://www.w3.org/TR/appmanifest/#dfn-standalone), но предоставляет конечному пользователю некоторые средства доступа к минимальному набору элементов пользовательского интерфейса для управления навигацией (например, назад, вперед, перезагрузка и, возможно, какой-то способ просмотра адреса документа). Пользовательский агент может включать в себя другие элементы пользовательского интерфейса, зависящие от платформы, такие как кнопки "поделиться" и "печать" или что-то еще, что обычно используется на платформе и в пользовательском агенте.
- [`standalone`](https://www.w3.org/TR/appmanifest/#dfn-standalone) - Открывает веб-приложение, чтобы оно выглядело как отдельное нативное приложение. Это может включать в себя наличие у приложения другого окна, собственной иконки в панели запуска приложений и т.д. В этом режиме пользовательский агент исключает стандартные элементы пользовательского интерфейса браузера, такие как строка URL-адреса, но может включать другие элементы пользовательского интерфейса системы, такие как строка состояния и/или системная кнопка возврата.
- [`fullscreen`](https://www.w3.org/TR/appmanifest/#dfn-fullscreen) - Открывает веб-приложение со скрытыми элементами пользовательского интерфейса браузера и занимает всю доступную область отображения.

У каждого режима отображения ([*display mode*](https://www.w3.org/TR/appmanifest/#dfn-display-mode)) есть резервная цепочка ([fallback chain](https://w3c.github.io/manifest/#dfn-fallback-chain)), представляющая собой список режимов отображения.

#### [`orientation`](https://www.w3.org/TR/appmanifest/#orientation-member)

Элемент [`orientation`](https://www.w3.org/TR/appmanifest/#orientation-member) - это строка, которая служит ориентацией экрана по умолчанию ([*default screen orientation*](https://www.w3.org/TR/screen-orientation/#dfn-default-screen-orientation)) для всех контекстов просмотра веб-приложения верхнего уровня ([*top-level browsing contexts*](https://html.spec.whatwg.org/multipage/document-sequences.html#top-level-browsing-context)). Возможными значениями являются значения перечисления [`OrientationLockType`](https://www.w3.org/TR/screen-orientation/#dom-orientationlocktype) (т.е. "any", "natural", "landscape", "portrait", "portrait-primary", "portrait-secondary", "landscape-primary", или "landscape-secondary").

[Подробнее про каждый тип ориентации приложения в пространстве можно прочитать тут 📂](../../core/html/topics/other-apis/topics/orientation/readme.md)

#### [`start_url`](https://www.w3.org/TR/appmanifest/#start_url-member)

Элемент [**`start_url`**](https://www.w3.org/TR/appmanifest/#start_url-member) - это строка, представляющая начальный URL-адрес, который разработчик предпочел бы, чтобы пользовательский агент загружал, когда пользователь запускает веб-приложение (например, когда пользователь нажимает на значок веб-приложения в меню приложений устройства или на рабочем столе).

Элемент [**`start_url`**](https://www.w3.org/TR/appmanifest/#start_url-member) является чисто рекомендательным, и пользовательский агент **МОЖЕТ (MAY)** проигнорировать его или предоставить конечному пользователю возможность не использовать его. Пользовательский агент **МОЖЕТ (MAY)** также разрешить конечному пользователю изменять URL-адрес, например, при создании закладки для веб-приложения или в любое другое время после этого.

#### [`id`](https://www.w3.org/TR/appmanifest/#id-member)

Элемент [**`id`**](https://www.w3.org/TR/appmanifest/#id-member) - это строка, представляющая идентификатор приложения. Идентификатор ([*identity*](https://w3c.github.io/manifest/#dfn-identity)) принимает форму URL-адреса, который имеет то же происхождение, что и [`start_url`](https://w3c.github.io/manifest/#dfn-start-url).

Идентификатор ([*identity*](https://w3c.github.io/manifest/#dfn-identity)) используется пользовательскими агентами для уникальной универсальной идентификации приложения. Когда пользовательский агент видит манифест с идентификатором ([*identity*](https://w3c.github.io/manifest/#dfn-identity)), который не соответствует уже установленному приложению, он **ДОЛЖЕН (SHOULD)** рассматривать этот манифест как описание отдельного приложения, даже если оно подается с того же URL-адреса, что и у другого приложения. Когда пользовательский агент видит манифест, в котором значение manifest["id"] равно идентификатору уже установленного приложения (при этом для параметра [exclude fragments](https://url.spec.whatwg.org/#url-equals-exclude-fragments) **НЕОБЯЗАТЕЛЬНО (OPTIONALLY)** задано значение true), это **ДОЛЖНО (SHOULD)** использоваться как сигнал о том, что этот манифест является заменой манифеста уже установленного приложения, а не заменой самого приложения. отдельное приложение, даже если оно подается с другого URL-адреса, отличного от того, который был показан ранее.

#### [`shortcuts`](https://www.w3.org/TR/appmanifest/#shortcuts-member)

Элемент [**`shortcuts`**](https://www.w3.org/TR/appmanifest/#shortcuts-member) - это список элементов быстрого доступа ([*shortcut item*](https://w3c.github.io/manifest/#dfn-shortcut-item)), которые предоставляют доступ к ключевым задачам в веб-приложении.

Способ представления элементов быстрого доступа (*shortcuts*) и количество из них, показываемых пользователю, определяется пользовательским агентом и/или операционной системой.

Пользовательский агент **ДОЛЖЕН (SHOULD)** отображать ярлыки с помощью взаимодействий, которые соответствуют отображению контекстного меню значка приложения в основной операционной системе (например, щелчок правой кнопкой мыши, длительное нажатие). Пользовательский агент **ДОЛЖЕН (SHOULD)** отображать ярлыки в том же порядке, в котором они указаны в манифесте. Агент пользователя **ДОЛЖЕН (SHOULD)** представлять сочетания клавиш таким образом, чтобы они соответствовали отображению контекстного меню значка приложения в операционной системе хоста. Агент пользователя **МОЖЕТ (MAY)** сократить список представленных сочетаний клавиш, чтобы сохранить соответствие соглашениям или ограничениям операционной системы хоста.

Каждый элемент быстрого доступа (*shortcut item*) представляет собой упорядоченную карту, которая представляет собой ссылку на ключевую задачу или страницу в веб-приложении. В нее входят следующие элементы:

- [`name`](https://w3c.github.io/manifest/#dfn-name-0) - это строка, представляющая название (*name*) элемента быстрого доступа в том виде, в каком оно обычно отображается пользователю в контекстном меню.
- [`short_name`](https://w3c.github.io/manifest/#dfn-short_name-0) - это строка, представляющая сокращенную версию названия быстрого доступа. Он предназначен для использования в тех случаях, когда недостаточно места для отображения полного имени быстрого доступа.
- [`description`](https://w3c.github.io/manifest/#dfn-description) - это строка, которая позволяет разработчику описать назначение элемента быстрого доступа (*shortcut*). Агенты пользователей **МОГУТ (MAY)** предоставлять эту информацию вспомогательным технологиям.
- [`url`](https://w3c.github.io/manifest/#dfn-url) - это URL-адрес в рамках обработанного ([*within scope*](https://w3c.github.io/manifest/#dfn-within-scope-0) of a [processed manifest](https://w3c.github.io/manifest/#dfn-processed-manifest)) манифеста, который открывается при активации связанного быстрого доступа.
- [`icons`](https://w3c.github.io/manifest/#dfn-icons-0) - это  изображения, которые служат символическими представлениями (*iconic representations*) быстрого доступа в различных контекстах.

[Примеры использования элемента **`shortcuts`** 📂](./examples/manifest-shortcuts.md)

### Color's members

#### [`theme_color`](https://www.w3.org/TR/appmanifest/#theme_color-member)

Элемент [**`theme_color`**](https://www.w3.org/TR/appmanifest/#theme_color-member) [^1] служит цветом темы по умолчанию для контекста приложения. Что представляет собой цвет темы, определено в [HTML](https://html.spec.whatwg.org/#meta-theme-color).

Если пользовательский агент принимает значение элемента [**`theme_color`**](https://www.w3.org/TR/appmanifest/#theme_color-member) в качестве цвета темы по умолчанию, то этот цвет служит цветом темы для всех контекстов просмотра, к которым применяется манифест. Однако документ может переопределить цвет темы по умолчанию, включив допустимый HTML элемент [`<meta>`](https://html.spec.whatwg.org/multipage/semantics.html#meta)), значение атрибута [`name`](https://html.spec.whatwg.org/multipage/semantics.html#attr-meta-name) которого равно [`"theme-color"`](https://html.spec.whatwg.org/multipage/semantics.html#meta-theme-color).

Пользовательский агент **МОЖЕТ (MAY)** игнорировать альфа-компонент ([*alpha component*](https://www.w3.org/TR/css-color-4/#alpha-channel)) цвета темы в зависимости от контекста. Например, в большинстве сред цвет темы не может быть прозрачным.

#### [`background_color`](https://www.w3.org/TR/appmanifest/#background_color-member)

Элемент [**`background_color`**](https://www.w3.org/TR/appmanifest/#background_color-member) [^1] описывает ожидаемый цвет фона веб-приложения. Он повторяет то, что уже доступно в таблице стилей (*stylesheet*) приложения, но может использоваться пользовательским агентом для отображения цвета фона веб-приложения, для которого манифест известен до того, как файлы станут доступны, независимо от того, были ли они получены из сети или с диска.

Элемент [**`background_color`**](https://www.w3.org/TR/appmanifest/#background_color-member) предназначен только для улучшения взаимодействия с пользователем во время загрузки веб-приложения и **НЕ ДОЛЖЕН (MUST NOT)** использоваться пользовательским агентом в качестве цвета фона (*background color*), когда доступна таблица стилей (*stylesheet*) веб-приложения.

### External application resource members

#### [`related_applications`](https://www.w3.org/TR/appmanifest/#related_applications-member)

Связанное приложение (*related application*) - это приложение, доступное для базовой прикладной платформы, которое имеет отношение к веб-приложению.

Элемент [**`related_applications`**](https://www.w3.org/TR/appmanifest/#related_applications-member) содержит список связанных приложений и служит указанием на такую связь между веб-приложением и связанными приложениями. Эта связь является однонаправленной, и если только указанное в списке приложение не претендует на такую же связь, пользовательский агент **НЕ ДОЛЖЕН (MUST NOT)** предполагать двунаправленного подтверждения.

Примером использования [**`related_applications`**](https://www.w3.org/TR/appmanifest/#related_applications-member) может быть поисковый робот (*crawler*), который будет использовать эту информацию для сбора дополнительной информации о веб-приложении, или браузер, который может предложить указанное приложение в качестве альтернативы, если пользователь захочет установить веб-приложение.

Ресурс внешнего приложения может содержать следующие элементы, некоторые из которых должны быть допустимыми для внешнего ресурса приложения:

- [`fingerprints`](https://w3c.github.io/manifest/#dfn-fingerprints)
- [`id`](https://w3c.github.io/manifest/#dfn-id-0)
- [`min_version`](https://w3c.github.io/manifest/#dfn-min_version)
- [`platform`](https://w3c.github.io/manifest/#dfn-platform) (**required**)
- [`url`](https://w3c.github.io/manifest/#dfn-url-0)

Допустимый ресурс внешнего приложения **ДОЛЖЕН (MUST)** содержать элемент платформы и либо [`url`](https://w3c.github.io/manifest/#dfn-url-0), либо [`id`](https://w3c.github.io/manifest/#dfn-id-0) элемента (или и то, и другое).

#### [`prefer_related_applications`](https://www.w3.org/TR/appmanifest/#prefer_related_applications-member)

Элемент [**`prefer_related_applications`**](https://www.w3.org/TR/appmanifest/#prefer_related_applications-member) - это логическое значение, которое используется в качестве подсказки для агента пользователя, указывающей, что связанные приложения должны быть предпочтительнее веб-приложения. Если для параметра [**`prefer_related_applications`**](https://www.w3.org/TR/appmanifest/#prefer_related_applications-member) установлено значение `true`, и пользовательский агент хочет предложить установить веб-приложение, то вместо этого пользовательский агент может захотеть предложить установить одно из связанных приложений ([*related applications*](https://w3c.github.io/manifest/#dfn-related-application)).

### [Application information members](https://www.w3.org/TR/manifest-app-info/)

Application information members - это дополнительные элементы, которые предоставляют дополнительные метаданные для манифеста приложения. Эти метаданные можно использовать в цифровом магазине или других местах, где это веб-приложение может продаваться или распространяться, или для улучшения диалога установки при установке веб-приложения.

Эти элементы классифицируются как дополнительные (*supplementary*), поскольку они не применяются к веб-приложению во время выполнения (*runtime*) (т.е. они носят чисто рекомендательный характер и не влияют на то, как пользовательский агент представляет установленное веб-приложение). Все элементы являются необязательными.

#### [`categories`](https://www.w3.org/TR/manifest-app-info/#categories-member)

Элемент [**`categories`**](https://www.w3.org/TR/manifest-app-info/#categories-member) представляет собой массив строк, описывающих категории приложений, к которым относится веб-приложение. Он предназначен в качестве подсказки для каталогов или магазинов, в которых представлены веб-приложения, и ожидается, что они приложат все усилия, чтобы найти подходящие категории (или разряд), в которые будет включено веб-приложение. Как и поисковые системы и мета-ключевые слова, каталоги и магазины не обязаны учитывать эту подсказку.

Полный список категории доступен по ссылке: <https://www.w3.org/TR/manifest-app-info/#categories-member>

#### [`description`](https://www.w3.org/TR/manifest-app-info/#description-member)

Элемент [**`description`**](https://www.w3.org/TR/manifest-app-info/#description-member) - это строка, которая позволяет разработчику описать назначение веб-приложения. Он служит доступным описанием ([*accessible description*](https://www.w3.org/TR/accname-1.2/#dfn-accessible-description)) установленного веб-приложения.

#### [`iarc_rating_id`](https://www.w3.org/TR/manifest-app-info/#iarc_rating_id-member)

Элемент [**`iarc_rating_id`**](https://www.w3.org/TR/manifest-app-info/#iarc_rating_id-member) - это строка, представляющая сертификационный код веб-приложения от Международной коалиции по оценке возраста ( International Age Rating Coalition (IARC)). Он предназначен для определения того, для какого возраста подходит веб-приложение.

Сертификат IARC, предназначенный для распространения веб-приложения, можно получить через участвующие в программе магазины. Члену [**`iarc_rating_id`**](<https://www.w3.org/TR/manifest-app-info/#iarc_rating_id-member>) требуется только один код сертификации. Один и тот же код может использоваться совместно всеми участвующими витринами, при условии, что распространяемый продукт остается неизменным (т.е. не использует совершенно разные пути ввода кода в зависимости от анализа агентом пользователя и тому подобного), а другие витрины поддерживают его.

#### [`screenshots`](https://www.w3.org/TR/manifest-app-info/#screenshots-member)

Элемент [**`screenshots`**](https://www.w3.org/TR/manifest-app-info/#screenshots-member) - это массив screenshot объектов, представляющих веб-приложение в распространенных сценариях использования.

По аналогии с элементом [`icons` 📂](#icons), элемент [**`screenshots`**](https://www.w3.org/TR/manifest-app-info/#screenshots-member) - это объект [`ImageResource`](https://www.w3.org/TR/image-resource/#dom-imageresource) с некоторыми дополнительными элементами, как определено ниже.

##### [`label`](https://www.w3.org/TR/manifest-app-info/#label-member)

Элемент [**`label`**](https://www.w3.org/TR/manifest-app-info/#label-member) - это строка, которая служит доступным именем для объекта screenshots. Для обеспечения доступности авторам рекомендуется указывать [**`label`**](https://www.w3.org/TR/manifest-app-info/#dfn-label) для каждого скриншота. Этот элемент может использоваться в качестве альтернативного текста для отображаемых скриншотов.

##### [`platform`](https://www.w3.org/TR/manifest-app-info/#platform-member)

Элемент [**`platform`**](https://www.w3.org/TR/manifest-app-info/#platform-member) - это строка, представляющая платформу распространения, к которой применим данный скриншот. Авторам рекомендуется использовать этот элемент только в том случае, если скриншот применим только в определенном контексте.

Пользовательские агенты могут показывать столько (или несколько) скриншотов, сколько они пожелают, но не должны показывать скриншоты, которые не относятся к их платформе (например, Google Play не должен показывать скриншоты, относящиеся к iOS).

Если платформа ([***`platform`***](https://www.w3.org/TR/manifest-app-info/#platform-member)) не задана, агенты пользователей должны предполагать, что скриншот применим ко всем платформам.

Полный список значений платформы, специфичных для конкретной операционной системы доступен по ссылке: <https://www.w3.org/TR/manifest-app-info/#platform-member>

##### [`form_factor`](https://www.w3.org/TR/manifest-app-info/#form_factor-member)

Элемент [**`form_factor`**](https://www.w3.org/TR/manifest-app-info/#form_factor-member) - это строка, представляющая форму экрана широкого класса устройств, для которых применим данный скриншот. Авторам рекомендуется использовать этот элемент только в том случае, если скриншот применим только в определенном контексте.

Пользовательские агенты могут показывать столько (или несколько) скриншотов, сколько они выберут, но не должны отображать скриншоты, которые не соответствуют их форм-фактору (например, мобильные телефоны не должны показывать "wide" скриншоты [**`form_factor`**](https://www.w3.org/TR/manifest-app-info/#form_factor-member)).

Если [**`form_factor`**](https://www.w3.org/TR/manifest-app-info/#form_factor-member) не задан, пользовательские агенты должны предполагать, что скриншот применим ко всем форм-факторам.

Список значений [**`form_factor`**](https://www.w3.org/TR/manifest-app-info/#form_factor-member):

- **narrow** - для скриншотов, применимых только к узким экранам (например, к мобильным устройствам).
- **wide** - для скриншотов, применимых только к широким экранам (например, к статусным таблицам (*status boards*)).

User agents might show as many (or as few) screenshots as they choose, but shouldn't display screenshots that do not pertain to their form factor (e.g., mobile phones shouldn't show "wide" `form_factor` screenshots).

## Events

- appinstalled

[^1]: Разработчики **МОГУТ (MAY)** переопределить значение, определенное цветового элемента, для поддержки prefers-color-scheme. Примеры.
