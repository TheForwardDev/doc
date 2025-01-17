# Json

- [Basics](#basics)
- [Field Set](#fields)
- [Key/Value Mode](#key-value)
- [Only Value Mode](#only-value)
- [Object Mode](#object-mode)
- [Default Value](#default)
- [Creatable/Removable](#creatable-removable)
- [Vertical Mode](#vertical)
- [Filter](#filter)
- [Buttons](#buttons)
- [Modifiers](#modify)

---

<a name="basics"></a>
## Basics

The `Json` field is designed for convenient work with the `json` data type. In most cases, it is used with arrays of objects via `TableBuilder`, but it also supports a mode for working with a single object.

> [!NOTE]
> In the database, the field must be of type `text` or `json`. It is also necessary to specify Eloquent Cast — `array`, `json`, or `collection`.

<a name="fields"></a>
## Field Set

Assume that the structure of your json looks like this:

`[{title: 'title', value: 'value', active: 'active'}]`

This is a set of objects with fields `title`, `value`, and `active`. To specify such a set of fields, the `fields` method is used:

```php
fields(FieldsContract|Closure|iterable $fields): static
```

Example usage:

```php
use MoonShine\UI\Fields\Json;
use MoonShine\UI\Fields\Position;
use MoonShine\UI\Fields\Switcher;
use MoonShine\UI\Fields\Text;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Product Options', 'options')
            ->fields([
                Position::make(),
                Text::make('Title'),
                Text::make('Value'),
                Switcher::make('Active')
            ])
    ];
}

// ...
```

![json_fields](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_fields.png)
![json_fields_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_fields_dark.png)

Fields can also be passed through a closure, allowing access to the field's context and its data:

```php
use MoonShine\UI\Fields\Json;
use MoonShine\UI\Fields\Position;
use MoonShine\UI\Fields\Switcher;
use MoonShine\UI\Fields\Text;

// ...

protected function indexFields(): iterable
{
    return [
        Json::make('Product Options', 'options')
            ->fields(static fn(Json $ctx) => $ctx->getData()->getOriginal()->is_active ? [
                Position::make(),
                Text::make('Title'),
                Text::make('Value'),
                Switcher::make('Active')
            ] : [
            Text::make('Title')
            ])
    ];
}

// ...
```

<a name="key-value"></a>
## Key/Value Mode

When your data has a key/value structure, like in the following example `{key: value}`, the `keyValue` method is used.

```php
keyValue(
    string $key = 'Key',
    string $value = 'Value',
    ?FieldContract $keyField = null,
    ?FieldContract $valueField = null,
)
```

- `$key` — the label for the "key" field,
- `$value` — the label for the "value" field,
- `$keyField` — the option to replace the "key" field with your own (default is `Text`),
- `$valueField` — the option to replace the "value" field with your own (default is `Text`).

Example usage:

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')->keyValue()
    ];
}

// ...
```

![json_key_value](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_key_value.png)
![json_key_value_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_key_value_dark.png)

Example with changing field types:

```php
use MoonShine\UI\Fields\Json;
use MoonShine\UI\Fields\Select;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Label', 'data')->keyValue(
            keyField: Select::make('Key')->options(['vk' => 'VK', 'email' => 'E-mail']),
            valueField: Select::make('Value')->options(['1' => '1', '2' => '2']),
        ),
    ];
}

// ...
```

<a name="only-value"></a>
## Only Value Mode

If you need to store only values, like in the example `['value_1', 'value_2']`, the `onlyValue()` method is used:

```php
onlyValue(
    string $value = 'Value',
    ?FieldContract $valueField = null,
)
```

- `$value` - the label for the "value" field,
- `$valueField` - the option to replace the "value" field with your own (default is `Text`).

Example usage:

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')->onlyValue()
    ];
}

// ...
```

![json_only_value](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_only_value.png)
![json_only_value_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_only_value_dark.png)

<a name="object-mode"></a>
## Object Mode

In most cases, the `Json` field works with an array of objects via `TableBuilder`. However, it is also possible to work with an object, for example, `{title: 'Title', active: false}`. For this, the `object()` method is used:

```php
object()
```

Example usage:

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Product Options', 'options')
            ->fields([
                Text::make('Title'),
                Switcher::make('Active')
            ])->object()
    ];
}

// ...
```

<a name="default"></a>
## Default Value

As in other fields, there is an option to specify a default value using the `default()` method. In this case, an array must be provided.

```php
default(mixed $default)
```

Example usage:

```php
use MoonShine\UI\Fields\Json;
use MoonShine\UI\Fields\Switcher;
use MoonShine\UI\Fields\Text;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')
            ->keyValue('Key', 'Value')
            ->default([
                [
                    'key' => 'Default key',
                    'value' => 'Default value'
                ]
            ]),

        Json::make('Product Options', 'options')
            ->fields([
                Text::make('Title'),
                Text::make('Value'),
                Switcher::make('Active')
            ])
            ->default([
                [
                    'title' => 'Default title',
                    'value' => 'Default value',
                    'active' => true
                ]
            ]),

        Json::make('Values')
            ->onlyValue()
            ->default([
                ['value' => 'Default value']
            ])
    ];
}

// ...
```

<a name="creatable-removable"></a>
## Creatable/Removable

By default, the `Json` field contains only one element. The `creatable()` method allows adding new elements, while `removable()` enables their removal.

Example usage:

```php
creatable(
    Closure|bool|null $condition = null,
    ?int $limit = null,
    ?ActionButtonContract $button = null
)
```

- `$condition` - condition under which the method should be applied,
- `$limit` - limit on the number of possible elements,
- `$button` - option to replace the add button with your own.

```php
removable(
    Closure|bool|null $condition = null,
    array $attributes = []
)
```

- `$condition` - condition under which the method should be applied,
- `$attributes` - HTML attributes for the remove button.

Example usage:

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')
            ->keyValue()
            ->creatable(limit: 6)
            ->removable()
    ];
}

// ...
```

![json_removable](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_removable.png)
![json_removable_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_removable_dark.png)

### Customizing the Add Button

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')
            ->keyValue()
            ->creatable(
                button: ActionButton::make('New', '#')->primary()
            )
    ];
}

// ...
```

### HTML Attributes for the Remove Button

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data', 'data.content')->fields([
            Text::make('Title'),
            Image::make('Image'),
            Text::make('Value'),
        ])
            ->removable(attributes: ['@click.prevent' => 'customAsyncRemove'])
            ->creatable()
    ];
}

// ...
```

<a name="vertical"></a>
## Vertical Mode

The `vertical()` method allows changing the display of the table from horizontal mode to vertical.

```php
vertical()
```

Example usage:

```php
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')
            ->keyValue()
            ->vertical()
    ];
}

// ...
```
![json_vertical](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_vertical.png)
![json_vertical_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/json_vertical_dark.png)

<a name="filter"></a>
## Application in Filters

If the field is used in filters, the filtering mode must be enabled using the `filterMode()` method. This method adapts the field's behavior for filtering and disables the ability to add new elements.

```php
use MoonShine\UI\Fields\Json;
use MoonShine\UI\Fields\Text;

// ...

public function filters(): array
{
    return [
        Json::make('Data')
            ->fields([
                Text::make('Title', 'title'),
                Text::make('Value', 'value')
            ])
            ->filterMode()
    ];
}

// ...
```

<a name="buttons"></a>
## Buttons

The `buttons()` method allows overriding the buttons used in the field. By default, only the remove button is available.

```php
buttons(array $buttons)
```

Example:

```php
use MoonShine\ActionButtons\ActionButton;
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data', 'data.content')->fields([
            Text::make('Title'),
            Image::make('Image'),
            Text::make('Value'),
        ])->buttons([
            ActionButton::make('', '#')
                ->icon('trash')
                ->onClick(fn() => 'remove()', 'prevent')
                ->secondary()
                ->showInLine()
        ])
    ];
}

// ...
```

<a name="modify"></a>
## Modifiers

The `Json` field provides the ability to modify buttons or the table in `preview` or `default` modes, instead of completely replacing them.

### Remove Button Modifier

The `modifyRemoveButton()` method allows changing the remove button.

```php
/**
 * @param  Closure(ActionButton $button, self $field): ActionButton  $callback
 */
modifyRemoveButton(Closure $callback)
```

Example:

```php
use MoonShine\ActionButtons\ActionButton;
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')
            ->modifyRemoveButton(
                fn(ActionButton $button) => $button->customAttributes([
                    'class' => 'btn-secondary'
                ])
            )
    ];
}

// ...
```

### Table Modifier

The `modifyTable()` method allows modifying the table (`TableBuilder`) for all visual modes of the field.

```php
/**
 * @param  Closure(TableBuilder $table, bool $preview): TableBuilder $callback
 */
modifyTable(Closure $callback)
```

Example:

```php
use MoonShine\Components\TableBuilder;
use MoonShine\UI\Fields\Json;

// ...

protected function formFields(): iterable
{
    return [
        Json::make('Data')
            ->modifyTable(
                fn(TableBuilder $table, bool $preview) => $table->customAttributes([
                    'style' => 'width: 50%;'
                ])
            )
    ];
}

// ...
```
