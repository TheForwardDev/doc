# Components

The `Components` component has no visual features; it is used for the quick output of a set of components.

You can create `Components` using the static method `make()` of the `Components` class.

```php
make(iterable $components = [])
```

`$components` - an array of components located in the header.

```php
use MoonShine\UI\Components\Components;

Components::make([
    // components
]);
```
