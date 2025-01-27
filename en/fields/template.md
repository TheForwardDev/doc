# Template

Contains all [Basic methods](/docs/{{version}}/fields/basic-methods).

`Template` field does not have a ready-made implementation and allows constructing a field using *fluent interface* during declaration.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use MoonShine\UI\Fields\Template;
use MoonShine\UI\Fields\Text;

Template::make()
    ->setLabel('My Field')
    ->fields([
        Text::make('Title')
    ])
```

> [!NOTE]
> Recipe: [HasOne through the Template Field](/docs/{{version}}/recipes/template).
