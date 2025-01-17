# ThemeSwitcher

Компонент *ThemeSwitcher* отображает кнопку-иконку для переключения темы (светлая/темная).

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
```blade
<x-moonshine::layout.theme-switcher />
```
~~~
