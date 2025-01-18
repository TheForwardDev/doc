# HasManyThrough

Inherits from [HasMany](/docs/{{version}}/fields/has-many).

\* has the same capabilities.

The `HasManyThrough` field is designed to work with the relationship of the same name in **Laravel**, inheriting from the `HasMany` field and including all its methods.

```php
use MoonShine\Laravel\Fields\Relationships\HasManyThrough;

HasManyThrough::make('Deployments', 'deployments', resource: DeploymentResource::class)
```
