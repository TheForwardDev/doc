# Template

Содержит все [Базовые методы](/docs/{{version}}/fields/basic-methods).

Поле `Template` не имеет готовой реализации и позволяет конструировать поле с помощью *fluent interface* в процессе объявления.

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
> Рецепт: [HasOne через поле Template](/docs/{{version}}/recipes/template).
