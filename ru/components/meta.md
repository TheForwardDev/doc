# Meta

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент **Meta** предназначен для размещения метаданных на html-странице.

```php
use MoonShine\UI\Components\Layout\Meta;

Meta::make('csrf-token')
    ->customAttributes([
        'content' => 'token',
    ]),
Meta::make()
    ->customAttributes([
        'name' => 'description',
        'content' => 'Page description',
    ]),
```

> [!NOTE]
> Родительский компонент: [Html](/docs/{{version}}/components/html).
