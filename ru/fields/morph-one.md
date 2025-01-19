# MorphOne

Наследует [HasOne](/docs/{{version}}/fields/has-one).

\* имеет те же возможности.

Поле отношения в **Laravel** типа `HasOne`.

```php
use MoonShine\Laravel\Fields\Relationships\MorphOne;

// ...

protected function fields(): iterable
{
    return [
        // ...
        MorphOne::make(
            'Profile',
            'profile',
            resource: ProfileResource::class
        )
    ];
}
```
