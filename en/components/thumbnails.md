# Thumbnails

To create thumbnails, you can use the `Thumbnails` component.

```php
make(array|FileItem|null|string $items)
```

- `$items` - thumbnail or a list of thumbnails.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Thumbnails;

Thumbnails::make([
    '/images/image_1.jpg',
    '/images/image_2.jpg',
    '/images/image_3.jpg',
]),
```
tab: Blade
```blade
<x-moonshine::thumbnails
    :items="[
        '/images/image_1.jpg',
        '/images/image_2.jpg',
        '/images/image_3.jpg',
    ]"
/>
```
~~~

You can specify only one thumbnail as string.

```blade
<x-moonshine::thumbnails
    :items="/images/thumb_1.jpg"
/>
```

You can also specify the `alt` attribute.

```blade
<x-moonshine::thumbnails
    :items="/images/thumb_1.jpg"
    alt="Description"
/>
```
