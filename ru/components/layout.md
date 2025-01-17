# Layout

Системный компонент *Layout* является стартовой точкой при создании шаблонов в **MoonShine** и используется единожды в методе `build()`.

Вы можете создать *Layout*, используя статический метод `make()` класса `Layout`.

```php
make(iterable $components = [])
```

`$components` - массив компонентов, которые располагаются в заголовке.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Layout;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout>
Any content
</x-moonshine::layout>
```
~~~
