# MorphToMany

Inherits [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

* has the same capabilities

The *BelongsToMany* relationship field in *Laravel*

The same as `MoonShine\Laravel\Fields\Relationships\BelongsToMany`, but for MorphToMany relationships `MoonShine\Laravel\Fields\Relationships\MorphToMany`.

```php
use MoonShine\Laravel\Fields\Relationships\MorphToMany;

// ...

protected function fields(): iterable
{
    return [
        MorphToMany::make('Categories', 'categories')
    ];
}

// ...
```
