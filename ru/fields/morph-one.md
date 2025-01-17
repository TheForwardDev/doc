# MorphOne

Наследует [HasOne](/docs/{{version}}/fields/has-one).

* имеет те же возможности

Поле отношения в **Laravel** типа *HasOne*.

То же самое, что `MoonShine\Laravel\Fields\Relationships\HasOne`, только для отношений *MorphOne*
`MoonShine\Laravel\Fields\Relationships\MorphOne`.

```php
use MoonShine\Laravel\Fields\Relationships\MorphOne;

// ...

protected function fields(): iterable
{
    return [
        MorphOne::make('Profile', 'profile')
    ];
}

// ...
```
