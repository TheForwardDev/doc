# Meta

> [!NOTE]
> Used to create **MoonShine** [layouts](/docs/{{version}}/appearance/layout).

The **Meta** component is designed to place metadata on html page.

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
> Parent component: [Html](/docs/{{version}}/components/html).
