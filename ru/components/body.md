# Body

Компонент `Body` используется для создания тега `<body>`.

```php
make(iterable $components = [])
```

`$components` - массив компонентов.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Body;

Body::make([
    // ...
])
```
tab: Blade
```bladehtml
<x-moonshine::layout.body>
    Any content
</x-moonshine::layout.body>
```
~~~
