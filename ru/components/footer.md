# Footer

- [Основы](#basics)
- [Авторские права](#copyright)
- [Меню](#menu)

---

<a name="basics"></a>
## Основы

Компонент `Footer` используется для создания блока подвала в **MoonShine**.

Вы можете создать `Footer`, используя статический метод `make()` класса `Footer`.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов, которые располагаются в подвале.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Footer;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...

            Footer::make([
                // ..
            ]),

            // ...
        ]);
    }
}
```
tab: Blade
```blade
<x-moonshine::layout.footer
    copyright="Your brand"
    :menu="['https://moonshine-laravel.com/docs' => 'Документация']"
>
Any content
</x-moonshine::layout.footer>
```
~~~

<a name="copyright"></a>
## Авторские права

Метод `copyright()` позволяет оформить блок авторских прав в подвале.

```php
copyright(string|Closure $text)
```

```php
Footer::make()->copyright(fn (): string => 'Your brand')
```

<a name="menu"></a>
## Меню

Метод `menu()` позволяет оформить блок меню в подвале.

```php
/**
 * @param  array<string, string>  $data
 */
menu(array $data)
```

- `$data` - массив элементов, где ключ - это url, а значение - название пункта меню.

```php
Footer::make()
    ->menu([
        'https://moonshine-laravel.com/docs' => 'Документация',
    ])
```
