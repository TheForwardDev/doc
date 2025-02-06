# TopBar

- [Basics](#basics)

---

<a name="basics"></a>
## Basics

The `TopBar` component is used to create a top navigation panel in **MoonShine**.

You can create a `TopBar` using the static method `make()` of the `TopBar` class.

```php
make(iterable $components = [])
```

The `make()` method takes an array of components as a parameter.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Menu;
use MoonShine\UI\Components\Layout\TopBar;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ..

            TopBar::make([
                Menu::make()->top()
            ]),

            // ...
        ]);
    }
}
```
tab: Blade
```bladehtml
<x-moonshine::layout.top-bar>
<x-moonshine::layout.menu :elements="[['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']]"/>
</x-moonshine::layout.top-bar>
```
~~~

![topbar](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/topbar.png#light)
![topbar_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/topbar_dark.png#dark)
