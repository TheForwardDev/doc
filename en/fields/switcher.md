# Switcher

Inherits from [Checkbox](/docs/{{version}}/fields/checkbox).

\* has the same features

The `Switcher` field is an extension of `Checkbox` with a different visual design.

~~~tabs
tab: Class
```php
use MoonShine\UI\Fields\Switcher;

Switcher::make('Publish', 'is_publish')
```
tab: Blade
```blade
<x-moonshine::form.wrapper label="Publish">
    <x-moonshine::form.switcher
        name="is_publish"
        :onValue="1"
        :offValue="0"
    />
</x-moonshine::form.wrapper>
```
~~~

![switcher](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/switcher.png#light)
![switcher_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/switcher_dark.png#dark)
