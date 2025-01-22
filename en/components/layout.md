# Layout

The system component `Layout` is the starting point when creating templates in **MoonShine** and is used once in the `build()` method.

You can create a `Layout` using the static method `make()` of the `Layout` class.

```php
make(iterable $components = [])
```

`$components` is an array of components that are placed in the header.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Layout;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout>
Any content
</x-moonshine::layout>
```
~~~
