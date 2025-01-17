# TopBar

- [Основы](#basics)

---

<a name="basics"></a>
## Основы

Компонент *TopBar* используется для создания верхней панели навигации в **MoonShine**.

Вы можете создать *TopBar*, используя статический метод `make()` класса `TopBar`.

```php
make(iterable $components = [])
```

В качестве параметра метод `make()` принимает массив с компонентами.

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
```blade
<x-moonshine::layout.top-bar>
<x-moonshine::layout.menu :elements="[['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']]"/>
</x-moonshine::layput.top-bar>
```
~~~

![topbar](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/topbar.png)
![topbar_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/topbar_dark.png)
