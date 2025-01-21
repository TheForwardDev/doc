# Dropdown

- [Basics](#basics)
- [Heading](#heading)
- [Footer](#footer)
- [Location](#location)

---

<a name="basics"></a>
## Basics

Using the `Dropdown` component, you can create dropdown blocks.

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

- $title - the title for the list inside the Dropdown
- $toggler - the appearance of the button to display
- $content - the content of the Dropdown
- $items - items for forming the list in the form of ul li
- $searchable - search by content
- $searchPlaceholder - placeholder for search
- $placement - location
- $footer - footer for the list inside the Dropdown

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
## Heading

```php
<x-moonshine::dropdown title="Dropdown title">
    <div class="m-4">
        {{ fake()->text() }}
    </div>
    <x-slot:toggler>Click me</x-slot:toggler>
</x-moonshine::dropdown>
```

<a name="footer"></a>
## Footer

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
## Location

Available locations:

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
> Additional placement options can be found in the official documentation [tippy.js](https://atomiks.github.io/tippyjs/v6/all-props/#placement).
