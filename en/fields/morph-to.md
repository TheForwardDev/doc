# MorphTo

Inherits from [BelongsTo](/docs/{{version}}/fields/belongs-to).

\* has the same capabilities.

The `MorphTo` relationship field in **Laravel**.

The same as `MoonShine\Laravel\Fields\Relationships\BelongsTo`, but for `MorphTo` relationships.

```php
use MoonShine\Laravel\Fields\Relationships\MorphTo;

// ...

protected function formFields(): iterable
{
    return [
        MorphTo::make('Commentable')->types([
            Article::class => 'title'
        ]),
    ];
}
// ...
```

![morph_to](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/morph_to.png)
![morph_to_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/morph_to_dark.png)

> [!TIP]
> The `types` method is required, specifying the available classes.

Description of the `types` method value:

Key - class-string<Model>
Value - string or array.

> [!TIP]
> If the value is passed as a string, it should point to the name of the field to be displayed.
> If passed as an array, the first element of the array is the name of the field to display, and the second is the relationship name instead of the model name.

```php
use MoonShine\Fields\Relationships\MorphTo;

// ...

public function fields(): array
{
    return [
        MorphTo::make('Imageable')->types([
            Company::class => ['short_name', 'Organization']
        ]),
    ];
}
```

![morph_to_array](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/morph_to_array.png)
![morph_to_array_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/morph_to_array_dark.png)
