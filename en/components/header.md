# Header

> [!NOTE]
> Used to create **MoonShine** [layouts](/docs/{{version}}/appearance/layout).

The `Header` component is designed to create a header block.

```php
make(iterable $components = [])
```

- `$components` - array of components.

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
