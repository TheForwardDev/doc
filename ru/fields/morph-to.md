# MorphTo

Наследует [BelongsTo](/docs/{{version}}/fields/belongs-to).

* имеет те же возможности

Поле отношения *MorphTo* в **Laravel**

То же самое, что `MoonShine\Laravel\Fields\Relationships\BelongsTo`, только для отношений *MorphTo*

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
> Требуется метод `types`, указывающий доступные классы.

Описание значения метода `types`:

Ключ - class-string<Model>
Значение - строка или массив.

> [!TIP]
> Если значение передаётся как строка, то она должна указывать на название поля, которое нужно отобразить.
> Если же передаётся как массив, то первый элемент массива — это название поля для отображения, а второй — имя отношения вместо названия модели.

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
// ...
```

![morph_to_array](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/morph_to_array.png)
![morph_to_array_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/morph_to_array_dark.png)
