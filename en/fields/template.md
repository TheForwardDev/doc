# Template

Contains all [Basic methods](/docs/{{version}}/fields/basic-methods).

`Template` field does not have a ready-made implementation and allows constructing a field using *fluent interface* during declaration.

```php
use MoonShine\UI\Fields\Template;
use MoonShine\UI\Fields\Text;

Template::make('MyField')
    ->setLabel('My Field')
    ->fields([
        Text::make('Title')
    ])
```
