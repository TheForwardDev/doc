# MorphToMany

Inherits [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

\* has the same capabilities.

Relationship field in **Laravel** of type `MorphToMany`.

```php
use MoonShine\Laravel\Fields\Relationships\MorphToMany;

MorphToMany::make(
    'Categories',
    'categories',
    resource: CategoryResource::class
)
```
