# MorphMany

Inherits from [HasMany](/docs/{{version}}/fields/has-many).

\* has the same capabilities.

A relationship field in **Laravel** of type `MorphMany`.

> [!WARNING]
> The `formatted` parameter is not used in the `MorphMany` field!

```php
use MoonShine\Laravel\Fields\Relationships\MorphMany;

// ...

protected function fields(): iterable
{
    return [
        // ...
        MorphMany::make('Comments', 'comments')
    ];
}
```
