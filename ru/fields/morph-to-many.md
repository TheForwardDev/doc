# MorphToMany

Наследует [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

\* имеет те же возможности.

Поле отношения `MorphToMany` в **Laravel**.

```php
use MoonShine\Laravel\Fields\Relationships\MorphToMany;

MorphToMany::make(
    'Categories',
    'categories',
    resource: CategoryResource::class
)
```
