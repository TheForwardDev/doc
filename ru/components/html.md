# Html

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `Html` служит основой для построения html-страницы.
Компонент является оберткой тега `<html>` и уже включает в себя `<!DOCTYPE html>`.

```php
make(array|iterable $components = [])
```

- `$components` - массив компонентов.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Html;

Html::make([
    Head::make([]),
    Body::make([]),
]);
```
tab: Blade
```blade
<x-moonshine::layout.html>
    <x-moonshine::layout.head />
    <x-moonshine::layout.body>
        // ...
    </x-moonshine::layout.body>
</x-moonshine::layout.html>
```
~~~

> [!NOTE]
> Дочерние компоненты: [Head](/docs/{{version}}/components/head), [Body](/docs/{{version}}/components/body).
