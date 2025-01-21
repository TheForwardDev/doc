# Body

The `Body` component is used to create a `body` block in **MoonShine**.

You can create a `Body` using the static method `make()` of the `Body` class.

```php
make(iterable $components = [])
```
`$components` - an array of components that are placed in the header.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Body;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...

            Body::make([])

            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout.body>
Any content
</x-moonshine::layout.body>
```
~~~
