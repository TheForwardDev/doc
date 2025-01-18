# MorphOne

Inherits from [HasOne](/docs/{{version}}/fields/has-one).

\* has the same capabilities.

Relationship field in **Laravel** of type `HasOne`.

The same as `MoonShine\Laravel\Fields\Relationships\HasOne`, but for `MorphOne` relationships.

```php
use MoonShine\Laravel\Fields\Relationships\MorphOne;

// ...

protected function fields(): iterable
{
    return [
        MorphOne::make('Profile', 'profile')
    ];
}
```
