# Link

- [Basics](#basics)
- [Tooltip](#tooltip)
- [Fill](#fill)
- [Icon](#icon)

---

<a name="basics"></a>
## Basics

To create a styled link, you can use the `Link` component.

```php
make(
    Closure|string $href,
    Closure|string $label = ''
)
```

- $href - link to the resource,
- $value - name of the link.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Link;

Link::make('https://moonshine-laravel.com', 'Moonshine')
```
tab: Blade
```bladehtml
<x-moonshine::link-button href="#">Link</x-moonshine::link-button>

<x-moonshine::link-native href="#">Link</x-moonshine::link-native>
```
~~~

<a name="tooltip"></a>
## Tooltip

To display a tooltip on hover, the `tooltip()` method is used.

```php
Link::make('https://moonshine-laravel.com', 'Moonshine')
    ->tooltip('Tooltip')
```

<a name="fill"></a>
## Fill

The `filled` parameter is responsible for the fill.

```php
Link::make('https://moonshine-laravel.com', 'Moonshine')
    ->filled()
```

```bladehtml
<x-moonshine::link-button
    href="#"
    :filled="true"
>
    Link
</x-moonshine::link-button>

<x-moonshine::link-native
    href="#"
    :filled="true"
>
    Link
</x-moonshine::link-native>
```

<a name="icon"></a>
## Icon

You can pass the `icon` parameter.

```php
Link::make('https://moonshine-laravel.com', 'Moonshine')
    ->icon('arrow-top-right-on-square')
```
