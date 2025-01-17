# Header

Компонент *Header* используется для создания блока заголовка в **MoonShine**.

Вы можете создать *Header*, используя статический метод `make()` класса `Header`.

```php
make(iterable $components = [])
```
`$components` - массив компонентов, которые располагаются в заголовке.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Header;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...

            Header::make([
                Search::make(),
            ]),

            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout.header>
Any content
</x-moonshine::layout.header>
```
~~~
