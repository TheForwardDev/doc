# Heading

- [Basics](#basics)
- [Gradation](#gradation)
- [Tag](#custom-tag)

---

<a name="basics"></a>
## Basics

The `Heading` component allows you to add headings to content.

```php
make(
    Closure|string $label = '',
    ?int $h = null,
    bool $asClass = true,
)
```

- `$label` - Value,
- `$h` - Gradation (1-6),
- `$asClass` - Use `<div>` with a gradation class or `h` tag.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Heading;

Heading::make('Title', 2)
```
tab: Blade
```blade
<x-moonshine::heading h="2">
    Hello world
</x-moonshine::heading>
```
~~~

<a name="gradation"></a>
## Gradation

Heading parameters can also be set using the `h()` method.

```php
h(int $gradation = 3, $asClass = true)
```

- `$gradation` - Gradation (1-6),
- `$asClass` - Use `<div>` with a gradation class or `h` tag.

```php
use MoonShine\UI\Components\Heading;

// <div class="h1">
Heading::make('Title')->h(1),
// <h1>
Heading::make('Title')->h(1, false),
// <div class="h3">
Heading::make('Title')->h(),
// <h3>
Heading::make('Title')->h(asClass: false),
```

<a name="custom-tag"></a>
## Tag

To change the heading tag, use the `tag()` method.

```php
tag(string $tag)
```

```php
// <p class="h2">
Heading::make('Title')
    ->tag('p')
    ->h(2),
```
