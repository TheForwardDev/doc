# Content

The *Content* component is used for the area that displays the content part of the page.

You can create *Content* using the static method `make()` of the `Content` class.

```php
make(iterable $components = [])
```

`$components` is an array of components that are placed in the header.

~~~tabs
tab: Class
```php
namespace App\MoonShine\Layouts;

use MoonShine\UI\Components\Layout\Content;

final class MoonShineLayout extends AppLayout
{
    public function build(): Layout
    {
        return Layout::make([
            // ...
            Content::make([
                Title::make($this->getPage()->getTitle())->class('mb-6'),
                Components::make(
                    $this->getPage()->getComponents()
                ),
            ])
            // ...
        ]);
    }
}
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
