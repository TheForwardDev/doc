# Logo

- [Основы](#basics)
- [Атрибуты](#attributes)

---

<a name="basics"></a>
## Основы

Компонент `Logo` отображает логотип вашей админ-панели.

Вы можете создать `Logo`, используя статический метод `make()`.

```php
make(
    string $href,
    string $logo,
    ?string $logoSmall = null,
    ?string $title = null,
    bool $minimized = false,
)
```

 - $href - адрес ссылки для перехода по клику на логотип,
 - $logo - ссылка на изображения логотипа,
 - $logoSmall - ссылка на уменьшенную версию логотипа,
 - $title - подсказа при наведении,
 - $minimized - взаимодействует с [Sidebar](/docs/{{version}}/components/sidebar). Если установлено true, то автоматически будет выбрано small logo.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Logo;

Logo::make(
    '/admin',
    '/vendor/moonshine/logo.svg',
    '/vendor/moonshine/logo-small.svg'
),
```
tab: Blade
```blade
<x-moonshine::layout.logo
    :href="'/admin'"
    :logo="'/vendor/moonshine/logo.svg'"
    :logoSmall="'/vendor/moonshine/logo-small.svg'"
/>
```
~~~

<a name="attributes"></a>
## Атрибуты

Для добавления атрибутов к тегу `img` у лого существуют два метода для двух режимов отображения - `logoAttributes()` и `logoSmallAttributes()`

```php
logoAttributes(array $attributes): self

logoSmallAttributes(array $attributes): self
```
