# TopBar

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `TopBar` предназначен для создания верхней панели навигации.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Menu;
use MoonShine\UI\Components\Layout\TopBar;

TopBar::make([
    Menu::make()->top()
])
```
tab: Blade
```blade
<x-moonshine::layout.top-bar>
    <x-moonshine::layout.menu
        :elements="[
            ['label' => 'Dashboard', 'url' => '/'],
            ['label' => 'Section', 'url' => '/section'],
        ]
    "/>
</x-moonshine::layout.top-bar>
```
~~~

![topbar](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/topbar.png#light)
![topbar_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/topbar_dark.png#dark)
