# BelongsTo

- [Basics](#basics)
- [Default Value](#default)
- [Nullable](#nullable)
- [Placeholder](#placeholder)
- [Creating Relation Object](#creatable)
- [Searching Values](#searchable)
- [Modifying Value Retrieval Query](#values-query)
- [Asynchronous Search](#async-search)
- [Associated Fields](#associated)
- [Values with Image](#with-image)
- [Options](#options)
- [Native Mode](#native)
- [Reactivity](#reactive)
- [Link](#link)

---

<a name="basics"></a>
## Basics

The _BelongsTo_ field is designed to work with the same-name relationship in Laravel and contains all [Basic Methods](/docs/{{version}}/fields/basic-methods).

To create this field, use the static method `make()`.

```php
BelongsTo::make(
    Closure|string $label,
    ?string $relationName = null,
    Closure|string|null $formatted = null,
    ModelResource|string|null $resource = null,
)
```

- `$label` - the label, the title of the field,
- `$relationName` - the name of the relation,
- `$formatted` - a closure or field in the related table for displaying values,
- `$resource` - the model resource that the relationship refers to.

> [!WARNING]
> The model resource that the relationship refers to is mandatory!
> The resource must also be registered in the _MoonShineServiceProvider_ service provider in the `$core->resources()` method. Otherwise, there will be a 500 error (Resource is required for MoonShine\Laravel\Fields\Relationships\BelongsTo...).


```php
use MoonShine\Laravel\Fields\Relationships\BelongsTo;

BelongsTo::make('Country', 'country', resource: CountryResource::class)
```

![belongs_to](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to.png)

![belongs_to_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_dark.png)

> [!NOTE]
> If `$relationName` is not specified, the relation name will be determined automatically based on `$label`.

```php
BelongsTo::make('Country', resource: CountryResource::class)
```

You can omit `$resource` if the model resource matches the relationship name.

```php
class CountryResource extends ModelResource
{
    // ...
}
// ...
BelongsTo::make('Country', 'country')
```

If you do not specify `$relationName`, the name of the relationship will be determined automatically based on `$label` (by camelCase rules).

```php
class CountryResource extends ModelResource
{
    // ...
}
// ...
BelongsTo::make('Country')
```

> [!NOTE]
> By default, the field used to display the value is the one specified by the `$column` property in the model resource.
> The `$formatted` argument allows overriding the $column property.

```php
namespace App\MoonShine\Resources;

use MoonShine\Laravel\Resources\ModelResource;

class CountryResource extends ModelResource
{
    public string $column = 'title';
}
// ...
BelongsTo::make(
    'Country',
    'country',
    formatted: 'name'
)
```

If you need to specify a more complex value for display, you can pass a callback function to the `$formatted` argument.

```php
BelongsTo::make(
    'Country',
    'country',
    fn($item) => "$item->id. $item->title"
)
```

If you need to change the column when working with models, use the `onAfterFill` method.

```php
BelongsTo::make(
    'Category',
    resource: CategoryResource::class
)->afterFill(fn($field) => $field->setColumn('changed_category_id'))
```

<a name="default"></a>
## Default Value

You can use the `default()` method if you need to specify a default value for the field.

```php
default(mixed $default)
```

You must pass a model object as the default value.

```php
use App\Models\Country;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;

BelongsTo::make('Country', resource: CategoryResource::class)
    ->default(Country::find(1))
```

<a name="nullable"></a>
## Nullable

As with all fields, if you need to store NULL, you should add the `nullable()` method.

```php
nullable(Closure|bool|null $condition = null)
```

```php
BelongsTo::make('Country', resource: CategoryResource::class)
    ->nullable()
```

![select_nullable](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/select_nullable.png)

![select_nullable_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/select_nullable_dark.png)

> [!TIP]
> **MoonShine** is a very convenient and functional tool. However, to use it, you need to be confident in the basics of Laravel.

Don't forget to specify in the database table that the field can accept a `Null` value.

<a name="placeholder"></a>
## Placeholder

The `placeholder()` method allows you to set the _placeholder_ attribute for the field.

```php
placeholder(string $value)
```

```php
BelongsTo::make('Country', 'country')
    ->nullable()
    ->placeholder('Country')
```

<a name="searchable"></a>
## Searching Values

If you need to search among values, you must add the `searchable()` method.

```php
use MoonShine\Laravel\Fields\Relationships\BelongsTo;
use App\MoonShine\Resources\CountryResource;

BelongsTo::make('Country', 'country', resource: CountryResource::class)
    ->searchable()
```

<a name="creatable"></a>
## Creating Relation Object

The `creatable()` method allows you to create a new relation object via a modal window.

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

You can customize the create button by passing the _button_ parameter to the method.

```php
BelongsTo::make('Author', resource: AuthorResource::class)
    ->creatable(
        button: ActionButton::make('Custom button', '')
    )
```

<a name="values-query"></a>
## Query for Values

The `valuesQuery()` method allows you to change the query to retrieve values.

```php
valuesQuery(Closure $callback)
```

```php
use Illuminate\Contracts\Database\Eloquent\Builder;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;

BelongsTo::make('Category', 'category', resource: CategoryResource::class)
    ->valuesQuery(fn(Builder $query, Field $field) => $query->where('active', true))
```

<a name="async-search"></a>
## Asynchronous Search

To implement asynchronous value search, use the `asyncSearch()` method.

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
> The search will be carried out by the field specified for the resource `column`. By default `column=id`.

You can pass parameters to the `asyncSearch()` method:
*   `$column` - the field by which the search is conducted,
*   `$searchQuery` - a callback function for filtering values,
*   `$formatted` - a callback function for customizing output,
*   `$associatedWith` - the field with which the association is established,
*   `$limit` - the number of items in the search results,
*   `$url` - the URL for processing the asynchronous request,

```php
use Illuminate\Contracts\Database\Eloquent\Builder;
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
> When building the query in `asyncSearchQuery()`, you can use the current values of the form. To do this, it is necessary to pass `Request` into the callback function.

```php
use Illuminate\Contracts\Database\Eloquent\Builder;
use Illuminate\Http\Request;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;
use MoonShine\UI\Fields\Select;

Select::make('Country', 'country_id'),
BelongsTo::make('City', 'city',  resource: CityResource::class)
    ->asyncSearch(
        'title',
        searchQuery: function (Builder $query, Request $request, Field $field): Builder {
            return $query->where('country_id', $request->get('country_id'));
        }
    )
```

> [!NOTE]
> When building the query in `asyncSearchQuery()`, the initial state of the builder is preserved.
If you need to replace it with your builder, use the `replaceQuery` flag.

```php
use Illuminate\Contracts\Database\Eloquent\Builder;
use Illuminate\Http\Request;
use MoonShine\Laravel\Fields\Relationships\BelongsTo;
use MoonShine\UI\Fields\Select;

Select::make('Country', 'country_id'),
BelongsTo::make('City', 'city',  resource: CityResource::class)
    ->asyncSearch(
        'title',
        asyncSearchQuery: function (Builder $query, Request $request, Field $field): Builder {
            return $query->where('country_id', $request->get('country_id'));
        },
        replaceQuery: true
    )
```

<a name="associated"></a>
## Associated Fields

To establish a relationship of selection values between fields, you can use the `associatedWith()` method.

```php
associatedWith(string $column, ?Closure $searchQuery = null)
```

- `$column` - the field with which the relationship is established,
- `$searchQuery` - a callback function for filtering values.

```php
BelongsTo::make('City', 'city', resource: CityResource::class)
    ->associatedWith('country_id')
```

> [!NOTE]
> For more complex configurations, you can use `asyncSearch()`.

<a name="with-image"></a>
## Values with Image

> [!NOTE]
> The `withImage()` method allows you to add an image to the value.

```php
withImage(
    string $column,
    string $disk = 'public',
    string $dir = ''
)
```

- `$column` - the field with the image,
- `$disk` - the file system disk,
- `$dir` - the directory relative to the root of the disk.

```php
BelongsTo::make('Country', resource: CountryResource::class)
    ->withImage('thumb', 'public', 'countries')
```

![belongs_to_image](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_image.png)

![belongs_to_image_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_image_dark.png)

<a name="options"></a>
## Options

All selection options are available for modification via *data attributes*:

```php
BelongsTo::make('Country', resource: CountryResource::class)
    ->searchable()
    ->customAttributes([
        'data-search-result-limit' => 5
    ])
```

> [!NOTE]
> For more detailed information, please refer to [Choices](https://choices-js.github.io/Choices/).

<a name="native"></a>
## Native Mode

The `native()` method disables the Choices.js library and displays the selection in native mode.

```php
BelongsTo::make('Type')->native()
```

<a name="reactive"></a>
## Reactivity

This field supports [reactivity](/docs/{{version}}/fields/basic-methods#reactive).

<a name="link"></a>
## Link

By default, *BelongsTo* links to the edit page, using the `link` method under the hood. If needed, you can override the `link`:

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
