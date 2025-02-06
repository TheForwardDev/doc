# Icon

- [Basics](#basics)
- [Custom Output](#custom)

---

<a name="basics"></a>
## Basics

The `Icon` component is used for rendering icons.

You can create an `Icon` using the static method `make()` of the `Icon` class.

```php
make(string $icon, int $size = 5, string|Color $color = '', ?string $path = null)
```

`$icon` - the name of the icon or HTML (if custom mode is used),
`$size` - size,
`$color` - color,
`$path` - the path to the directory where the Blade templates for icons are located.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Icon;

Icon::make('users');
```
tab: Blade
```bladehtml
<x-moonshine::icon icon="users" />
```
~~~

<a name="custom"></a>
## Custom Output

Example with passing an HTML icon:

```php
Icon::make(svg('path-to-icon-pack')->toHtml())->custom(),
```
