# MorphMany

Inherits from [HasMany](/docs/{{version}}/fields/has-many).

* has the same capabilities

A relationship field in *Laravel* of type *morphMany*

The same as `MoonShine\Laravel\Fields\Relationships\HasMany`, but for *morphMany* relationships in `MoonShine\Laravel\Fields\Relationships\MorphMany`

> [!WARNING]
> The `formatted` parameter is not used in the `MorphMany` field!

```php
use MoonShine\Laravel\Fields\Relationships\MorphMany;

// ...

protected function fields(): iterable
{
    return [
        MorphMany::make('Comments', 'comments')
    ];
}

// ...
```
