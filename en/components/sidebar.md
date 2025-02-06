# Sidebar

- [Basics](#basics)
- [Collapsible Option](#collapsed)

---

<a name="basics"></a>
## Basics

The `Sidebar` component is used to create a side menu in **MoonShine**.

You can create a `Sidebar` using the static method `make()` of the `Sidebar` class.

```php
make(iterable $components = [])
```

The `make()` method takes an array of components as a parameter.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Menu;
use MoonShine\UI\Components\Layout\Sidebar;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ..

            Sidebar::make([
                Menu::make(),
            ])->collapsed(),

            // ...
        ]);
    }
}
```
tab: Blade
```bladehtml
<x-moonshine::layout.sidebar :collapsed="true">
<x-moonshine::layout.menu :elements="[['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']]"/>
</x-moonshine::layout.sidebar>
```
~~~

<a name="collapsed"></a>
## Collapsible Option

By default, the `Sidebar` is always open, but using the `collapsed()` method, you can add the option to hide the `Sidebar`:

```php
Sidebar::make([
    Menu::make(),
])->collapsed(),
```
