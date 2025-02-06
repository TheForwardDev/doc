# ThemeSwitcher

The *ThemeSwitcher* component displays a button-icon for switching themes (light/dark).

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\ThemeSwitcher;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...
            Div::make([
                ThemeSwitcher::make(),

                Div::make([
                    Burger::make(),
                ])->class('menu-heading-burger'),
            ])->class('menu-heading-actions'),
            // ...
        ]);
    }
}
```
tab: Blade
```bladehtml
<x-moonshine::layout.theme-switcher />
```
~~~
