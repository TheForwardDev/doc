# Spinner

- [Основы](#basics)
- [Размер](#size)
- [Цвет](#color)
- [Позиционирование](#position)

---

<a name="basics"></a>
## Основы

Используя компонент `Spinner`, вы можете создавать индикаторы загрузки.

```php
make(
    string $size = 'sm',
    string|Color $color = '',
    bool $fixed = false,
    bool $absolute = false,
)
```

- $size - размер,
- $color - цвет,
- $fixed - позиция fixed,
- $absolute - позиция absolute.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Spinner;

Spinner::make()
```
tab: Blade
```blade
<x-moonshine::spinner size="md" />
```
~~~

<a name="size"></a>
## Размер

Доступные размеры:

- sm
- md
- lg
- xl

```php
<x-moonshine::spinner size="sm" />
<x-moonshine::spinner size="md" />
<x-moonshine::spinner size="lg" />
<x-moonshine::spinner size="xl" />
```

<a name="color"></a>
## Цвет

Доступные цвета:

<span class="badge badge-primary">primary</span>
<span class="badge badge-secondary">secondary</span>
<span class="badge badge-success">success</span>
<span class="badge badge-warning">warning</span>
<span class="badge badge-error">error</span>
<span class="badge badge-info">info</span>

```php
<x-moonshine::spinner color="primary" />
<x-moonshine::spinner color="secondary" />
<x-moonshine::spinner color="success" />
<x-moonshine::spinner color="warning" />
<x-moonshine::spinner color="error" />
<x-moonshine::spinner color="info" />
```

<a name="position"></a>
## Позиционирование

Параметр `absolute="true"` задает абсолютное позиционирование индикатора загрузки.

```php
<x-moonshine::spinner :absolute="true" />
```

Параметр `fixed="true"` задает фиксированное позиционирование индикатора загрузки.

```php
<x-moonshine::spinner :fixed="true" />
```
