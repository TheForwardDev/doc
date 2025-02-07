# MobileBar

> [!NOTE]
> Used to create **MoonShine** [layouts](/docs/{{version}}/appearance/layout).

The `MobileBar` component is necessary if you want to customize the mobile dropdown panel according to your needs,
as by default it duplicates the content of the `TopBar` or `Sidebar`.

```php
make(iterable $components = [])
```

- `$components` - array of components.

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
