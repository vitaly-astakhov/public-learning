# Cache

## [Cache](https://www.rfc-editor.org/rfc/rfc9110#name-caches)
**Cache** - это локальное хранилище (**local store**) предыдущих ответных сообщений (**response messages**) и подсистема, управляющая хранением, извлечением и удалением сообщений. Кэш хранит кэшируемые ответы, чтобы сократить время отклика и потребление пропускной способности сети при будущих эквивалентных запросах.


Cache может быть двух видов: **shared cache** и **private cache**

**Shared cache (общий кэш)** - это кэш, в котором хранятся ответы для повторного использования более чем одним пользователем. Shared cache обычно, но не всегда, развертываются в составе посредника (**intermediary**)

**Private cache (частный кэш)** - это кэш, который предназначен для одного пользователя. Часто они развертываются как компонент агента пользователя (**user agent**)




A "shared cache" is a cache that stores responses for reuse by more than one user; shared caches are usually (but not always) deployed as a part of an intermediary. A "private cache", in contrast, is dedicated to a single user; often, they are deployed as a component of a user agent

«Общий кэш» — это кэш, в котором хранятся ответы для повторного использования более чем одним пользователем; Общие кэши обычно (но не всегда) развертываются в составе посредника. «Частный кэш», напротив, предназначен для одного пользователя; Часто они развертываются как компонент Агент пользователя
