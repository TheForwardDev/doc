# MobileBar

- [Basics](#basics)

---

<a name="basics"></a>
## Basics

The *MobileBar* component is necessary if you want to customize the mobile dropdown panel according to your needs,
as by default it duplicates the content of the `TopBar` or `Sidebar`.

You can create a *MobileBar* using the static method `make()` of the `MobileBar` class.

```php
make(iterable $components = [])
```

As a parameter, the `make()` method accepts an array of components.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Menu;
use MoonShine\UI\Components\Layout\MobileBar;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ..

            MobileBar::make([
                Menu::make()
            ]),

            // ...
        ]);
    }
}
```
tab: Blade
```bladehtml
<x-moonshine::layout.mobile-bar>
<x-moonshine::layout.menu :elements="[['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']]"/>
</x-moonshine::layput.mobile-bar>
```
~~~
