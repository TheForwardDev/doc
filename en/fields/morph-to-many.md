# MorphToMany

Inherits [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

\* has the same capabilities.

The `MorphToMany` relationship field in **Laravel**.

```php
use MoonShine\Laravel\Fields\Relationships\MorphToMany;

MorphToMany::make(
    'Categories',
    'categories',
    resource: CategoryResource::class
)
```
