# Dropdown

- [Основы](#basics)
- [Заголовок](#heading)
- [Подвал](#footer)
- [Расположение](#location)

---

<a name="basics"></a>
## Основы

Используя компонент `Dropdown`, вы можете создавать выпадающие блоки.

```php
make(
    ?string $title = null,
    Closure|string $toggler = '',
    Closure|Renderable|string $content = '',
    Closure|array $items = [],
    bool $searchable = false,
    Closure|string $searchPlaceholder = '',
    string $placement = 'bottom-start',
    Closure|string $footer = '',
)
```

- $title - заголовок для списка внутри Dropdown
- $toggler - внешний вид кнопки для отображения
- $content - контент Dropdown
- $items - элементы, для формирования списка вида ul li
- $searchable - поиск по контенту
- $searchPlaceholder - placeholder для поиска
- $placement - расположение
- $footer - footer для списка внутри Dropdown

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Dropdown;

Dropdown::make(
    'Dropdown',
    'Toggler',
    'Content',
    ['Item 1', 'Item 1']
)
```
tab: Blade
```blade
<x-moonshine::dropdown>
    <div class="m-4">
        {{ fake()->text() }}
    </div>
    <x-slot:toggler>Click me</x-slot:toggler>
</x-moonshine::dropdown>
```
~~~

<a name="heading"></a>
## Заголовок

```php
<x-moonshine::dropdown title="Dropdown title">
    <div class="m-4">
        {{ fake()->text() }}
    </div>
    <x-slot:toggler>Click me</x-slot:toggler>
</x-moonshine::dropdown>
```

<a name="footer"></a>
## Подвал

```php
<x-moonshine::dropdown>
    <div class="m-4">
        {{ fake()->text() }}
    </div>
    <x-slot:toggler>Click me</x-slot:toggler>
    <x-slot:footer>Dropdown footer</x-slot:footer>
</x-moonshine::dropdown>
```

<a name="location"></a>
## Расположение

Доступные расположения:

- bottom,
- top,
- left,
- right.

```php
<x-moonshine::dropdown placement="left">
    <div class="m-4">
        {{ fake()->text() }}
    </div>
    <x-slot:toggler>Click me</x-slot:toggler>
</x-moonshine::dropdown>
```

> [!NOTE]
> Дополнительные варианты расположения можно найти в официальной документации [tippy.js](https://atomiks.github.io/tippyjs/v6/all-props/#placement).
