# Body

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `Body` предназначен для создания тега `<body>`.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Body;

Body::make([
    // ...
])
```
tab: Blade
```blade
<x-moonshine::layout.body>
    Any content
</x-moonshine::layout.body>
```
~~~
