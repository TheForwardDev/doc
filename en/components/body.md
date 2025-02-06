# Body

The `Body` component is used to create a `<body>` tag.

```php
make(iterable $components = [])
```

`$components` - array of components.

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
