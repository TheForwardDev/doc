# Wrapper

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `Wrapper` используется как обвертка, чтобы боковая панель и контентная часть отображались корректно.
Используется сразу после `Body`.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Body;
use MoonShine\UI\Components\Layout\Wrapper;

Body::make([
    Wrapper::make([])
])
```
tab: Blade
```blade
<x-moonshine::layout.body>
    <x-moonshine::layout.wrapper>
        Content
    </x-moonshine::layout.wrapper>
</x-moonshine::layout.body>
```
~~~
