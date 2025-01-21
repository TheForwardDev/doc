# Components

Компонент `Components` не имеет визуальных особенностей, используется для быстрого вывода набора компонентов

Вы можете создать `Components`, используя статический метод `make()` класса `Components`.

```php
make(iterable $components = [])
```

`$components` - массив компонентов, которые располагаются в заголовке.

```php
use MoonShine\UI\Components\Components;

Components::make([
    // components
]);
```
