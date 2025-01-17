# Header

The *Header* component is used to create a header block in **MoonShine**.

You can create a *Header* using the static `make()` method of the `Header` class.

```php
make(iterable $components = [])
```
`$components` is an array of components that are placed in the header.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Header;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...

            Header::make([
                Search::make(),
            ]),

            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout.header>
Any content
</x-moonshine::layout.header>
```
~~~
