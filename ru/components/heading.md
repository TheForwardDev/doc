# Heading

- [Основы](#basics)
- [Градация](#gradation)
- [Тег](#custom-tag)

---

<a name="basics"></a>
## Основы

Компонент `Heading` позволяет добавлять заголовки к контенту.

```php
make(
    Closure|string $label = '',
    ?int $h = null,
    bool $asClass = true,
)
```

`$label` - Значение,
`$h` - Градация (1-6),
`$asClass` - Использовать `<div>` с классом градации или тег `h`.

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
## Градация

Параметры заголовка так же можно задать с помощью метода `h()`.

```php
h(int $gradation = 3, $asClass = true)
```

`$gradation` - Градация (1-6),
`$asClass` - Использовать `<div>` с классом градации или тег `h`.

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
## Тег

Чтобы изменить тег заголовка, воспользуйтесь методом `tag()`.

```php
tag(string $tag)
```

```php
// <p class="h2">
Heading::make('Title', 2)
    ->tag('p'),

// <p>
Heading::make('Title', 2, false)
    ->tag('p'),
```
