# MobileBar

- [Основы](#basics)

---

<a name="basics"></a>
## Основы

Компонент *MobileBar* необходим если вы хотите кастомизировать мобильную выпадающую панель по своему,
так как по умолчанию дублируется содержимое `TopBar` или `Sidebar`.

Вы можете создать *MobileBar*, используя статический метод `make()` класса `MobileBar`.

```php
make(iterable $components = [])
```

В качестве параметра метод `make()` принимает массив с компонентами.

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
