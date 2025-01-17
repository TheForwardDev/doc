# Wrapper

The *Wrapper* component is used as a wrapper to ensure that the sidebar and content part are displayed correctly. It is used immediately after the *Body*.

You can create a *Wrapper* using the static method `make()` of the `Wrapper` class.

```php
make(iterable $components = [])
```

`$components` is an array of components that are placed in the header.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Wrapper;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...
            Body::make([
                Wrapper::make([
                    // ...
                ])
            ]),
            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout.body>
    <x-moonshine::layout.wrapper>
    </x-moonshine::layout.wrapper>
</x-moonshine::layout.body>
```
~~~
