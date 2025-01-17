# Html

The **Html** component serves as the foundation for building an html page in MoonShine. \
The component is a wrapper for the `<html>` tag and already includes `<!DOCTYPE html>`.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Html;

Html::make(array|iterable $components = []);
```
```php
Html::make([
    Head::make(),
    Body::make([
        // ...
    ])
]);
```
tab: Blade
```blade
<x-moonshine::layout.html>
    <x-moonshine::layout.head />
    <x-moonshine::layout.body>
        // ...
    </x-moonshine::layout.body>
</x-moonshine::layout.html>
```
~~~

> [!TIP]
> Child components: [Head](/docs/{{version}}/components/head), [Body](/docs/{{version}}/components/body)
