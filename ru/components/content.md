# Content

Компонент `Content` используется для области с отображением контентной части страницы.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов.

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
