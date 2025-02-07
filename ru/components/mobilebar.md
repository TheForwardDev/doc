# MobileBar

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `MobileBar` необходим если вы хотите кастомизировать мобильную выпадающую панель по своему,
так как по умолчанию дублируется содержимое `TopBar` или `Sidebar`.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Menu;
use MoonShine\UI\Components\Layout\MobileBar;

MobileBar::make([
    Menu::make(),
])
```
tab: Blade
```blade
<x-moonshine::layout.mobile-bar>
    <x-moonshine::layout.menu
        :elements="[
            ['label' => 'Dashboard', 'url' => '/'],
            ['label' => 'Section', 'url' => '/section'],
        ]"
    />
</x-moonshine::layput.mobile-bar>
```
~~~
