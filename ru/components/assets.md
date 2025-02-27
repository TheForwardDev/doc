# Assets

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `Assets` предназначен для подключения к html-странице скриптов и таблиц стилей, добавленных через [AssetManager](/docs/{{version}}/appearance/assets).

> [!NOTE]
> Компонент `Assets` также подключает системные стили и скрипты.

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

> [!NOTE]
> Родительский компонент: [Head](/docs/{{version}}/components/head).
