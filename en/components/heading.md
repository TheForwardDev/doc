# Heading

- [Basics](#basics)
- [Gradation](#gradation)
- [Wrapper Tag](#wrapper-tag)

---

<a name="basics"></a>
## Basics

The `Heading` component allows you to add headings to content.

```php
make(
    Closure|string $label = '',
    ?int $h = null,
    bool $asClass = true
)
```

`$label` - Value,
`$h` - Gradation,
`$asClass` - Use as a div with a gradation class or an `h` tag.

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

```php
h(int $gradation = 3, $asClass = true)
```

The method allows wrapping the content in *h1 - h6* tag or in a *div* with a gradation class.
The first parameter defines the gradation of the tag, the second defines whether to use a tag or a class for *div*.

```php
use MoonShine\UI\Components\Heading;

// Will be tags h1 - h4
Heading::make('Dashboard')->h(1, false),
Heading::make('MoonShine')->h(2, false),
Heading::make('Demo version')->h(asClass: false),
Heading::make('Heading')->h(4, false),

// Will be div.h1 - div.h4
Heading::make('Dashboard')->h(1),
Heading::make('MoonShine')->h(2),
Heading::make('Demo version')->h(), // h3
Heading::make('Heading')->h(4),
```

<a name="wrapper-tag"></a>
## Wrapper Tag

```php
tag(string $tag)
```

The method allows wrapping the content in the specified tag.

```php
Heading::make('Dashboard')->tag('p')->h(1),
Heading::make('MoonShine')->tag('p')->h(2),
Heading::make('Demo version')->tag('p')->h(),
Heading::make('Heading')->tag('p')->h(4),
```
