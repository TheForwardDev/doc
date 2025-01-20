# MorphOne

Наследует [HasOne](/docs/{{version}}/fields/has-one).

\* имеет те же возможности.

Поле отношения в **Laravel** типа `HasOne`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use App\MoonShine\Resources\ProfileResource;
use MoonShine\Laravel\Fields\Relationships\MorphOne;

MorphOne::make(
    'Profile',
    'profile',
    resource: ProfileResource::class
)
```
