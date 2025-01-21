# Burger

Компонент `Burger` отображает кнопку-иконку для отображения мобильного меню.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Burger;

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
```blade
<x-moonshine::layout.burger />
```
~~~
