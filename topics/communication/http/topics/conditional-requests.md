# [Conditional Requests](https://www.rfc-editor.org/rfc/rfc9110.html#section-13)

**Условный запрос (Conditional Request)** - это HTTP-запрос с одним или несколькими полями заголовка запроса, которые указывают на предварительные условия (**preconditions**), которые должны соблюдаться перед применением метода запроса к целевому ресурсу

**Preconditions** - Это поля, которе состоят из сравнения набора валидаторов, полученных из предыдущих представлений целевого ресурса, с текущим состоянием валидаторов для выбранного представления

## Use cases

- [Обновление кэша (Cache update)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests#cache_update)
- [Интеграция частичной загрузки](https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests#integrity_of_a_partial_download)
- [Avoiding the lost update problem with optimistic locking](https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests#avoiding_the_lost_update_problem_with_optimistic_locking)
- [Dealing with the first upload of a resource](https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests#dealing_with_the_first_upload_of_a_resource)

### Поля

Когда исходный сервер (**origin server**) получает запрос (**request**), который выбирает представление (**representation**), и этот запрос включает поле заголовка с условием (`If-*`), исходный сервер (**origin server**) **ДОЛЖЕН (MUST)** оценить переданное условие (`If-*`) согласно [разделу 13.2](https://www.rfc-editor.org/rfc/rfc9110.html#section-13.2) перед выполнением метода.

У полей, которые влияют на **conditional request**, есть своя приоритетность. [Подробнее можно ознакомиться тут](https://www.rfc-editor.org/rfc/rfc9110#section-13.2.2).

### [If-Match](https://www.rfc-editor.org/rfc/rfc9110.html#section-13.1.1) 🎩

**If-Match** - Запрос с этим полем выполняется успешно, если `ETag` удаленного ресурса равен значению, указанному в этом заголовке. Выполняется строгая проверка.

Это поле чаще всего используется с изменяющими состояние методами (POST, PUT, PATCH, DELETE) для предотвращения случайных перезаписей, когда несколько пользовательских агентов могут действовать параллельно на одном и том же ресурсе (т.е. для предотвращения проблемы "потерянного обновления" (**"lost update"**)).

### [If-None-Match](https://www.rfc-editor.org/rfc/rfc9110.html#section-13.1.3) 🎩

**If-None-Match** - Запрос с этим полем выполняется успешно, если `ETag` удаленного ресурса отличается от каждого из перечисленных в этом заголовке. Выполняется слабая проверка.

Это поле в основном используется в условных запросах с методом GET, чтобы обеспечить эффективное обновление кэшированной информации с минимальными затратами на транзакцию.

### [If-Modified-Since](https://www.rfc-editor.org/rfc/rfc9110.html#section-13.1.3) 🎩

**If-Modified-Since** - Запрос с этим полем выполняется успешно, если поле `Last-Modified` удаленного ресурса более поздняя, чем указанная в этом заголовке.

Получатель **ДОЛЖЕН (MUST)** игнорировать поле заголовка `If-Modified-Since`, если запрос содержит поле заголовка `If-None-Match`, так как у него приоритетность выше, чем у поля `If-Modified-Since`.

### [If-Unmodified-Since](https://www.rfc-editor.org/rfc/rfc9110.html#section-13.1.4) 🎩

**If-Unmodified-Since** - Запрос с этим полем выполняется успешно, если поле `Last-Modified` удаленного ресурса старше или совпадает с датой, указанной в этом заголовке.

### [If-Range](https://www.rfc-editor.org/rfc/rfc9110.html#section-13.1.5) 🎩

Исходный сервер (**origin server**), который вычисляет условие `If-Match`, **НЕ ДОЛЖЕН (MUST NOT)** выполнять запрошенный метод, если условие имеет значение false.
