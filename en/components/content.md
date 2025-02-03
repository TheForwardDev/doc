# Content

The `Content` component is used for the area that displays the content part of the page.

```php
make(iterable $components = [])
```

- `$components` - array of components.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Content;

Content::make([
    Title::make(
        $this->getPage()->getTitle()
    ),

    Components::make(
        $this->getPage()->getComponents()
    ),
])
```
tab: Blade
```blade
<x-moonshine::layout.content>
    <article class="article">
        Content
    </article>
</x-moonshine::layout.content>
```
~~~
