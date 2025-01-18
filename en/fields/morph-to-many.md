# MorphToMany

Inherits [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

\* has the same capabilities.

The `MorphToMany` relationship field in **Laravel**.

```php
use MoonShine\Laravel\Fields\Relationships\MorphToMany;

// ...

protected function fields(): iterable
{
    return [
        // ...
        MorphToMany::make('Categories', 'categories')
    ];
}
```
