# Assets

The `Assets` component is used to include scripts and stylesheets into the HTML page, added through [AssetManager](/docs/{{version}}/appearance/assets).

> [!NOTE]
> The `Assets` component also includes system styles and scripts.

~~~tabs
tab: Class
```php
use MoonShine\UI\Components\Layout\Assets;

Assets::make();
```
tab: Blade
```blade
<x-moonshine::layout.assets />
```
~~~

> [!TIP]
> Parent component: [head](/docs/{{version}}/components/head)
