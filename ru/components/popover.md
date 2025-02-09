# Popover

- [Основы](#basics)
- [Без использования компонента](#without)

---

<a name="basics"></a>
## Основы

Используя компонент `Popover`, вы можете создать всплывающее окно.

```php
make(
    string $title,
    string $trigger,
    string $placement = 'right',
)
```

Доступные расположения:

- `bottom`,
- `top`,
- `left`,
- `right`.

~~~tabs
tab: Class
```php
Popover::make('Title', 'Trigger')
    ->content('HTML content')
```
tab: Blade
```blade
<x-moonshine::popover title="Popover title" placement="right">
    <x-slot:trigger>
        <button class="btn">Popover</button>
    </x-slot:trigger>
    <p>This is a very beautiful popover, show some love.</p>
    <div class='flex justify-between mt-3'>
        <button type='button' class='btn btn-sm'>Skip</button>
        <button type='button' class='btn btn-sm btn-primary'>Read More</button>
    </div>
</x-moonshine::popover>
```
~~~

<a name="without"></a>
## Без использования компонента

```html
<span x-data="popover" data-content="HTML HERE">
    <a class="text-purple font-semibold">Popover 1</a>
</span>
```

или

```html
<span
    x-data="popover({placement: 'top'})"
    title="Popover title"
    data-content="HTML HERE">
    <a class="text-purple font-semibold">Popover 2</a>
</span>
```
