# Rating

Компонент `Rating` позволяет создавать стилизованные рейтинги.

Вы можете создать `Rating`, используя статический метод `make()`.

```php
make(
    int $value,
    int $min = 1,
    int $max = 5
)
```
- $value - значение рейтинга,
- $min - минимальное значение,
- $$max - максимальное значение.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Rating;

Rating::make(3, 1, 10)
```
tab: Blade
```blade
<x-moonshine::rating value="8" min="1" max="10" />
```
~~~
