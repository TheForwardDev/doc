# Wrapper

Компонент `Wrapper` используется как обвертка, чтобы боковая панель и контентная часть отображались корректно.
Используется сразу после `Body`.

Вы можете создать `Wrapper`, используя статический метод `make()` класса `Wrapper`.

```php
make(iterable $components = [])
```

`$components` - массив компонентов, которые располагаются в заголовке.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Wrapper;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...
            Body::make([
                Wrapper::make([
                    // ...
                ])
            ]),
            // ...
        ]);
    }
}
```
tab: Blade
```bladehtml
<x-moonshine::layout.body>
    <x-moonshine::layout.wrapper>
    </x-moonshine::layout.wrapper>
</x-moonshine::layout.body>
```
~~~
