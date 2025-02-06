# Header

The `Header` component is used to create a header block in **MoonShine**.

```php
make(iterable $components = [])
```
`$components` - an array of components that are placed in the header.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Header;

Header::make([
    Search::make(),
])
```
tab: Blade
```blade
<x-moonshine::layout.header>
    Any content
</x-moonshine::layout.header>
```
~~~
