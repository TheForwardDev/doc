# Content

Компонент *Content* используется для области с отображением контентной части страницы.

Вы можете создать *Content*, используя статический метод `make()` класса `Content`.

```php
make(iterable $components = [])
```

`$components` - массив компонентов, которые располагаются в заголовке.

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
