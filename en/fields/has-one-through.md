# HasOneThrough

Inherits from [HasOne](/docs/{{version}}/fields/has-one).

\* has the same capabilities.

The `HasOneThrough` field is designed to work with the relationship of the same name in **Laravel**, inheriting from the `HasOne` field and including all its methods.

```php
use MoonShine\Laravel\Fields\Relationships\HasOneThrough;

HasOneThrough::make('Car owner', 'carOwner', resource: new OwnerResource::class)
```
