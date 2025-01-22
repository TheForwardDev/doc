# Html

Компонент `Html` служит основой для построения html-страницы в **MoonShine**.
Компонент является оберткой тега `<html>` и уже включает в себя `<!DOCTYPE html>`.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Html;

Html::make(array|iterable $components = []);
```
```php
Html::make([
    Head::make(),
    Body::make([
        // ...
    ])
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

> [!TIP]
> Дочерние компоненты: [Head](/docs/{{version}}/components/head), [Body](/docs/{{version}}/components/body).
