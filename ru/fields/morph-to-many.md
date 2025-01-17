# MorphToMany

Наследует [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

* имеет те же возможности

Поле отношения *BelongsToMany* в **Laravel**

То же самое, что `MoonShine\Laravel\Fields\Relationships\BelongsToMany`, только для отношений MorphToMany `MoonShine\Laravel\Fields\Relationships\MorphToMany`.

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
