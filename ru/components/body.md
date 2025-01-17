# Body

Компонент *Body* используется для создания блока `body` в **MoonShine**.

Вы можете создать *Body*, используя статический метод `make()` класса `Body`.

```php
make(iterable $components = [])
```
`$components` - массив компонентов, которые располагаются в заголовке.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Body;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...

            Body::make([])

            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout.body>
Any content
</x-moonshine::layout.body>
```
~~~
