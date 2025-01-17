# Footer

- [Basics](#basics)
- [Copyright](#copyright)
- [Menu](#menu)

---

<a name="basics"></a>
## Basics

The *Footer* component is used to create a footer block in **MoonShine**.

You can create a *Footer* using the static method `make()` of the `Footer` class.

```php
make(iterable $components = [])
```

- `$components` - an array of components that are placed in the footer.

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
    :menu="['https://moonshine-laravel.com/docs' => 'Documentation']"
>
Any content
</x-moonshine::layout.footer>
```
~~~

<a name="copyright"></a>
## Copyright

The method `copyright()` allows you to create a copyright block in the footer.

```php
copyright(string|Closure $text)
```

```php
Footer::make()->copyright(fn (): string => 'Your brand')
```

<a name="menu"></a>
## Menu

The method `menu()` allows you to create a menu block in the footer.

```php
/**
 * @param  array<string, string>  $data
 */
menu(array $data)
```

- `$data` - an array of items where the key is the URL, and the value is the name of the menu item.

```php
Footer::make()
    ->menu([
        'https://moonshine-laravel.com/docs' => 'Documentation',
    ])
```
