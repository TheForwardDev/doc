# Heading

- [Основы](#basics)
- [Градация](#gradation)
- [Тег](#custom-tag)

---

<a name="basics"></a>
## Основы

Компонент `Heading` позволяет добавлять заголовки к контенту.

Вы можете создать `Heading`, используя статический метод `make()` класса `Heading`.

```php
make(Closure|string $label = '', ?int $h = null, bool $asClass = true)
```

`$label` - Значение,
`$h` - Градация,
`$asClass` - Использовать как div с классом градации или тег `h`,

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Heading;

Heading::make('Title')->h(2);
```
tab: Blade
```blade
<x-moonshine::heading h="2">Hello world</x-moonshine::heading>
```
~~~

<a name="gradation"></a>
## Градация

```php
h(int $gradation = 3, $asClass = true)
```

Метод позволяет обернуть содержимое в тег *h1 - h6* или в *div* с классом градации.
Первый параметр определяет градацию тега, второй определяет, использовать ли тег или класс для *div*.

```php
use MoonShine\UI\Components\Heading;

// Будут теги h1 - h4
Heading::make('Панель управления')->h(1, false),
Heading::make('MoonShine')->h(2, false),
Heading::make('Демо версия')->h(asClass: false),
Heading::make('Заголовок')->h(4, false),

// Будут div.h1 - div.h4
Heading::make('Панель управления')->h(1),
Heading::make('MoonShine')->h(2),
Heading::make('Демо версия')->h(), // h3
Heading::make('Заголовок')->h(4),
```

<a name="custom-tag"></a>
## Тег

```php
tag(string $tag)
```

Метод позволяет обернуть содержимое в указанный тег.

```php
Heading::make('Панель управления')->tag('p')->h(1),
Heading::make('MoonShine')->tag('p')->h(2),
Heading::make('Демо версия')->tag('p')->h(),
Heading::make('Заголовок')->tag('p')->h(4),
```
