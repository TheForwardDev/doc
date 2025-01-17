# Sidebar

- [Основы](#basics)
- [Возможность скрыть](#collapsed)

---

<a name="basics"></a>
## Основы

Компонент *Sidebar* используется для создания бокового меню в **MoonShine**.

Вы можете создать *Sidebar*, используя статический метод `make()` класса `Sidebar`.

```php
make(iterable $components = [])
```

Метод `make()` принимает в качестве параметра массив компонентов.

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
```blade
<x-moonshine::layout.sidebar :collapsed="true">
<x-moonshine::layout.menu :elements="[['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']]"/>
</x-moonshine::layput.sidebar>
```
~~~

<a name="collapsed"></a>
## Возможность скрыть

По умолчанию *Sidebar* всегда открыт, но с помощью метода `collapsed()`, вы можете добавить возможность скрыть *Sidebar*:

```php
Sidebar::make([
    Menu::make(),
])->collapsed(),
```
