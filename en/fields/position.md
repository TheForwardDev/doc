# Position

Inherits [Preview](/docs/{{version}}/fields/preview).

* has the same capabilities

The *Position* field allows you to create numbering for repeating elements.

```php
use MoonShine\UI\Fields\Json;
use MoonShine\UI\Fields\Position;
use MoonShine\UI\Fields\Switcher;
use MoonShine\UI\Fields\Text;

Json::make('Product Options', 'options')
    ->fields([
        Position::make(),
        Text::make('Title'),
        Text::make('Value'),
        Switcher::make('Active')
    ])
```
