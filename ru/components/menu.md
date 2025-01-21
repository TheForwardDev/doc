# Menu

- [Основы](#basics)
- [Режим горизонтальное меню](#top)
- [Прокрутка к активному пункту](#scroll-to)

---

<a name="basics"></a>
## Основы

Компонент `Menu` создает меню на основе `MenuManager` или переданных элементов меню.

Вы можете создать меню, используя статический метод `make()` класса `Menu`.

```php
make(?iterable $elements = [])
```

`$elements` - набор элементов меню, если пусто за основу берет `MenuManager`.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Body;

Menu::make([
    MenuItem::make('Item', '/')
]);
```
tab: Blade
```blade
<x-moonshine::layout.menu :elements="[['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']]" :top="false" :scroll-to="false" />
```
~~~

Также можно инициализировать меню через примитивный массив:

```php
Menu::make([['label' => 'Dashboard', 'url' => '/'], ['label' => 'Section', 'url' => '/section']])
```

<a name="top"></a>
## Режим горизонтальное меню

Если вы решили расположить меню в горизонтальном режиме в *TopBar*, то воспользуйтесь методом `top()`:

```php
Menu::make()->top()
```

<a name="scroll-to"></a>
## Режим горизонтальное меню

По умолчанию если меню не в режиме *top*, то происходит скролл к активному пункту меню, но это поведение можно отключить с помощью метода `withoutScrollTo()`:

```php
Menu::make()->withoutScrollTo()
```

Чтобы включить обратно:

```php
Menu::make()->scrollTo()
```
