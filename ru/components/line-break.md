# LineBreak

Компонент `LineBreak` добавляет вертикальный отступ между элементами.

Вы можете создать `LineBreak`, используя статический метод `make()`.

```php
make(string $name = 'default')
```

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\LineBreak;

LineBreak::make(),
```
tab: Blade
```blade
<x-moonshine::layout.line-break/>
```
~~~
