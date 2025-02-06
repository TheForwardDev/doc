# Title

Компонент *Title* используется для основного заголовка страницы.

Вы можете создать *Title*, используя статический метод `make()` класса `Title`.

```php
make(Closure|string|null $value, int $h = 1)
```

`$value` - Значение,
`$h` - Градация,

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Title;

Title::make('Hello world');
```
tab: Blade
```blade
<x-moonshine::title>Hello world</x-moonshine::title>
```
~~~
