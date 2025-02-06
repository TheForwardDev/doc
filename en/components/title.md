# Title

The *Title* component is used for the main page header.

You can create a *Title* using the static method `make()` of the `Title` class.

```php
make(Closure|string|null $value, int $h = 1)
```

`$value` - Value,
`$h` - Level,

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Title;

Title::make('Hello world');
```
tab: Blade
```bladehtml
<x-moonshine::title>Hello world</x-moonshine::title>
```
~~~
