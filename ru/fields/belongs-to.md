# BelongsTo

- [Основы](#basics)
- [Значение по умолчанию](#default)
- [Nullable](#nullable)
- [Подсказка](#placeholder)
- [Создание объекта связи](#creatable)
- [Поиск значений](#searchable)
- [Изменение запроса получения значений](#values-query)
- [Асинхронный поиск](#async-search)
- [Связанные поля](#associated)
- [Значения с изображением](#with-image)
- [Опции](#options)
- [Нативный режим](#native)
- [Реактивность](#reactive)
- [Ссылка](#link)

---

<a name="basics"></a>
## Основы

Поле `BelongsTo` предназначено для работы с одноименной связью в **Laravel** и включает все [Базовые методы](/docs/{{version}}/fields/basic-methods).

```php
BelongsTo::make(
    Closure|string $label,
    ?string $relationName = null,
    Closure|string|null $formatted = null,
    ModelResource|string|null $resource = null,
)
```

- `$label` - метка, заголовок поля,
- `$relationName` - название связи,
- `$formatted` - замыкание или поле в связанной таблице для отображения значений,
- `$resource` - `ModelResource`, на которую ссылается связь.

> [!WARNING]
> Наличие `ModelResource`, на который ссылается отношение, обязательно.
> Ресурс также необходимо [зарегистрировать](/docs/{{version}}/model-resource/index#declaring-in-the-system) в сервис-провайдере `MoonShineServiceProvider` в методе `$core->resources()`.
> В противном случае будет ошибка 500 (Resource is required for MoonShine\Laravel\Fields\Relationships\BelongsTo...).

```php
use MoonShine\Laravel\Fields\Relationships\BelongsTo;

BelongsTo::make('Country', 'country', resource: CountryResource::class)
```

![belongs_to](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to.png)
![belongs_to_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_dark.png)

Вы можете опустить `$resource`, если `ModelResource` совпадает с названием связи.

```php
class CountryResource extends ModelResource
{
    // ...
}

// ...

BelongsTo::make('Country', 'country')
```

Если не указать `$relationName`, то имя связи будет определено автоматически на основе `$label` (по правилам camelCase).

```php
class CountryResource extends ModelResource
{
    // ...
}

// ...

BelongsTo::make('Country')
```

> [!NOTE]
> По умолчанию, для отображения значения используется поле в связанной таблице, которое указано свойством `$column` в `ModelResource`.
> Аргумент `$formatted` позволяет переопределить свойство `$column`.

```php
class CountryResource extends ModelResource
{
    public string $column = 'title';

    // ...
}

// ...

BelongsTo::make(
    'Country',
    'country',
    formatted: 'name'
)
```

Если необходимо указать более сложное значение для отображения, то в аргумент `$formatted` можно передать функцию обратного вызова.

```php
BelongsTo::make(
    'Country',
    'country',
    fn($item) => "$item->id. $item->title"
)
```

Если необходимо изменить колонку при работе с моделями, используйте метод `onAfterFill()`.

```php
BelongsTo::make(
    'Category',
    resource: CategoryResource::class
)->afterFill(fn($field) => $field->setColumn('changed_category_id'))
```

<a name="default"></a>
## Значение по умолчанию

Вы можете использовать метод `default()`, если вам нужно указать значение по умолчанию для поля.

```php
default(mixed $default)
```

Вы должны передать объект модели в качестве значения по умолчанию.

```php
BelongsTo::make('Country', resource: CategoryResource::class)
    ->default(Country::find(1))
```

<a name="nullable"></a>
## Nullable

Как и для всех полей, если необходимо хранить NULL, нужно добавить метод `nullable()`.

```php
nullable(Closure|bool|null $condition = null)
```

```php
BelongsTo::make('Country', resource: CategoryResource::class)
    ->nullable()
```

![select_nullable](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/select_nullable.png)
![select_nullable_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/select_nullable_dark.png)

Не забудьте указать в таблице базы данных, что поле может принимать значение `Null`.

<a name="placeholder"></a>
## Подсказка

Метод `placeholder()` позволяет установить атрибут _placeholder_ у поля.

```php
placeholder(string $value)
```

```php
BelongsTo::make('Country', 'country')
    ->nullable()
    ->placeholder('Country')
```

<a name="searchable"></a>
## Поиск значений

Если необходимо осуществлять поиск среди значений, нужно добавить метод `searchable()`.

```php
BelongsTo::make('Country', 'country', resource: CountryResource::class)
    ->searchable()
```

<a name="creatable"></a>
## Создание объекта связи

Метод `creatable()` позволяет создать новый объект связи через модальное окно.

```php
creatable(
    Closure|bool|null $condition = null,
    ?ActionButton $button = null,
)
```

```php
BelongsTo::make('Author', resource: AuthorResource::class)
    ->creatable()
```

![belongs_to_creatable](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_creatable.png)
![belongs_to_creatable_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_creatable_dark.png)

Вы можете настроить кнопку создания, передав параметр _button_ в метод.

```php
BelongsTo::make('Author', resource: AuthorResource::class)
    ->creatable(
        button: ActionButton::make('Custom button', '')
    )
```

<a name="values-query"></a>
## Запрос для значений

Метод `valuesQuery()` позволяет изменить запрос для получения значений.

```php
valuesQuery(Closure $callback)
```

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:4]
use App\MoonShine\Resources\CategoryResource;
use Illuminate\Contracts\Database\Eloquent\Builder;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;
use MoonShine\UI\Fields\Field;

BelongsTo::make('Category', 'category', resource: CategoryResource::class)
    ->valuesQuery(fn(Builder $query, Field $field) => $query->where('active', true))
```

<a name="async-search"></a>
## Асинхронный поиск

Для реализации асинхронного поиска значений используйте метод `asyncSearch()`.

```php
asyncSearch(
    string $column = null,
    ?Closure $searchQuery = null,
    ?Closure $formatted = null,
    ?string $associatedWith = null,
    int $limit = 15,
    ?string $url = null,
)
```

```php
BelongsTo::make('Country', 'country', resource: CategoryResource::class)
    ->asyncSearch()
```

> [!TIP]
> Поиск будет осуществляться по полю связи ресурса `column`.
> По умолчанию `column=id`.

Вы можете передать параметры в метод `asyncSearch()`:

*   `$column` - поле, по которому осуществляется поиск,
*   `$searchQuery` - функция обратного вызова для фильтрации значений,
*   `$formatted` - функция обратного вызова для настройки вывода,
*   `$associatedWith` - поле, с которым установить связь,
*   `$limit` - количество элементов в результатах поиска,
*   `$url` - url для обработки асинхронного запроса.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:4]
use Illuminate\Contracts\Database\Eloquent\Builder;
use Illuminate\Http\Request;
use MoonShine\UI\Fields\Field;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;

BelongsTo::make('Country', 'country', resource: CategoryResource::class)
    ->asyncSearch(
        'title',
        searchQuery: function (Builder $query, Request $request, Field $field) {
            return $query->where('id', '!=', 2);
        },
        formatted: function ($country, Field $field) {
            return $country->id . ' | ' . $country->title;
        },
        limit: 10,
        url: 'https://moonshine-laravel.com/async'
    )
```

> [!NOTE]
> При построении запроса в `asyncSearchQuery()` можно использовать текущие значения формы.
> Для этого необходимо передать `Request` в функцию обратного вызова.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:5]
use Illuminate\Contracts\Database\Eloquent\Builder;
use Illuminate\Http\Request;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;
use MoonShine\UI\Fields\Field;
use MoonShine\UI\Fields\Select;

protected function fields(): iterable
{
    return [
        // ...
        Select::make('Country', 'country_id'),
        BelongsTo::make('City', 'city',  resource: CityResource::class)
            ->asyncSearch(
                'title',
                searchQuery: function (Builder $query, Request $request, Field $field): Builder {
                    return $query->where('country_id', $request->get('country_id'));
                }
            )
    ];
}
```

> [!NOTE]
> При построении запроса в `asyncSearchQuery()` сохраняется исходное состояние построителя.
> Если вам нужно заменить его своим построителем, то используйте флаг `replaceQuery`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:5]
use Illuminate\Contracts\Database\Eloquent\Builder;
use Illuminate\Http\Request;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;
use MoonShine\UI\Fields\Field;
use MoonShine\UI\Fields\Select;

protected function fields(): iterable
{
    return [
        // ...
        Select::make('Country', 'country_id'),
        BelongsTo::make('City', 'city',  resource: CityResource::class)
            ->asyncSearch(
                'title',
                asyncSearchQuery: function (Builder $query, Request $request, Field $field): Builder {
                    return $query->where('country_id', $request->get('country_id'));
                },
                replaceQuery: true
            )
    ];
}
```

<a name="associated"></a>
## Связанные поля

Для установления связи значений выбора между полями можно использовать метод `associatedWith()`.

```php
associatedWith(string $column, ?Closure $searchQuery = null)
```

- `$column` - поле, с которым устанавливается связь,
- `$searchQuery` - функция обратного вызова для фильтрации значений.

```php
BelongsTo::make('City', 'city', resource: CityResource::class)
    ->associatedWith('country_id')
```

> [!NOTE]
> Для более сложной настройки вы можете использовать `asyncSearch()`.

<a name="with-image"></a>
## Значения с изображением

> [!NOTE]
> Метод `withImage()` позволяет добавить изображение к значению.

```php
withImage(
    string $column,
    string $disk = 'public',
    string $dir = ''
)
```

- `$column` - поле с изображением,
- `$disk` - диск файловой системы,
- `$dir` - директория относительно корня диска.

```php
BelongsTo::make('Country', resource: CountryResource::class)
    ->withImage('thumb', 'public', 'countries')
```

![belongs_to_image](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_image.png)
![belongs_to_image_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_image_dark.png)

<a name="options"></a>
## Опции

Все опции выбора доступны для изменения через *атрибуты data*:

```php
BelongsTo::make('Country', resource: CountryResource::class)
    ->searchable()
    ->customAttributes([
        'data-search-result-limit' => 5
    ])
```

> [!NOTE]
> Для получения более подробной информации, пожалуйста, обратитесь к [Choices](https://choices-js.github.io/Choices/).

<a name="native"></a>
## Нативный режим

Метод `native()` отключает библиотеку Choices.js и отображает выбор в нативном режиме.

```php
BelongsTo::make('Type')->native()
```

<a name="reactive"></a>
## Реактивность

Данному полю доступна [реактивность](/docs/{{version}}/fields/basic-methods#reactive).

<a name="link"></a>
## Ссылка

По умолчанию, `BelongsTo` ссылается на страницу редактирования.
Вы можете переопределить это поведение с помощью метода `link()`.

```php
BelongsTo::make(
    __('moonshine::ui.resource.role'),
    'moonshineUserRole',
    resource: MoonShineUserRoleResource::class,
)
->link(
    link: fn(string $value, BelongsTo $ctx) => $ctx->getResource()->getDetailPageUrl($ctx->getData()->getKey()),
    name: fn(string $value) => $value,
    icon: 'users',
    blank: true,
)
```
