# MorphToMany

Наследует [BelongsToMany](/docs/{{version}}/fields/belongs-to-many).

\* имеет те же возможности.

Поле отношения `MorphToMany` в **Laravel**.

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
