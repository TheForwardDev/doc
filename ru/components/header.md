# Header

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `Header` предназначен для создания блока заголовка.

```php
make(iterable $components = [])
```
`$components` - массив компонентов, которые располагаются в заголовке.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Header;

Header::make([
    Search::make(),
])
```
tab: Blade
```blade
<x-moonshine::layout.header>
    Any content
</x-moonshine::layout.header>
```
~~~
