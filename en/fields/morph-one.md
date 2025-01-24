# MorphOne

Inherits from [HasOne](/docs/{{version}}/fields/has-one).

\* has the same capabilities.

Relationship field in **Laravel** of type `MorphOne`.

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
