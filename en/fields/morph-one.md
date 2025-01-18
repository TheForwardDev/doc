# MorphOne

Inherits from [HasOne](/docs/{{version}}/fields/has-one).

\* has the same capabilities.

Relationship field in **Laravel** of type `HasOne`.

```php
use MoonShine\Laravel\Fields\Relationships\MorphOne;

// ...

protected function fields(): iterable
{
    return [
        // ...
        MorphOne::make('Profile', 'profile')
    ];
}
```
