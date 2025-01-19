# MorphMany

Наследует [HasMany](/docs/{{version}}/fields/has-many).

\* имеет те же возможности.

Поле отношения в **Laravel** типа `MorphMany`.

> [!WARNING]
> Параметр `formatted` не используется в поле `MorphMany`!

```php
use MoonShine\Laravel\Fields\Relationships\MorphMany;

// ...

protected function fields(): iterable
{
    return [
        // ...
        MorphMany::make(
            'Comments',
            'comments',
            resource: CommentResource::class
        )
    ];
}
```
