# TinyMce

- [Installation](#installation)
- [Basics](#basics)
- [Default Config](#default-config)
- [Locale](#locale)
- [Plugins](#plugins)
- [Menubar](#menubar)
- [Toolbar](#toolbar)
- [Options](#options)
- [File Manager](#file-manager)

---

Inherits [Textarea](/docs/{{version}}/fields/textarea).

* has the same capabilities

> [!WARNING]
> Before using this field, you must register on the [Tiny.Cloud](https://www.tiny.cloud) website, obtain a token, and add it to your `.env`.

```
TINYMCE_TOKEN="YOUR_TOKEN"
```

---

<a name="installation"></a>
## Installation

```shell
composer require moonshine/tinymce
```

<a name="basics"></a>
## Basics

```php
use MoonShine\TinyMce\Fields\TinyMce;

TinyMce::make('Description')
```

<a name="default-config"></a>
## Default Config

The `TinyMce` field by default uses the most commonly used settings, such as plugins, menubar, and toolbar.

To change the default settings, you need to publish the configuration file:

```php
php artisan vendor:publish --tag="moonshine-tinymce-config"
```

You can also add additional parameters to the configuration file that will be applied to all `TinyMce` fields.

```php
'options' => [
    'forced_root_block' => 'div',
    'force_br_newlines' => true,
    'force_p_newlines' => false,
],
```

<a name="locale"></a>
## Locale

By default, the locale of your application is used, but you can specify a specific locale with the `locale()` method.

```php
locale(string $locale)
```
```php
TinyMce::make('Description')
    ->locale('ru');
```

Currently, English (en), Russian (ru), and Ukrainian (uk) are available, but we are always ready to add others.

If you want to add new localizations, create a task or submit a pull request.

<a name="plugins"></a>
## Plugins

The `plugins()` method allows you to completely override the plugins that will be used by the field.

```php
plugins(array $plugins)
```
```php
TinyMce::make('Description')
    ->plugins(['code', 'image', 'link', 'media', 'table'])
```

The `addPlugins()` method allows you to add new plugins to the default plugins.

```php
addPlugins(array $plugins)
```
```php
TinyMce::make('Description')
    ->addPlugins(['wordcount'])
```

The `removePlugins()` method allows you to exclude plugins that will be used in the field.

```php
removePlugins(array $plugins)
```
```php
TinyMce::make('Description')
    ->removePlugins(['autoresize'])
```

<a name="menubar"></a>
## Menubar

The `menubar()` method allows you to completely override the menu bar for the field.

```php
menubar(string|bool $menubar)
```
```php
TinyMce::make('Description')
    ->menubar('file edit view')
```

<a name="toolbar"></a>
## Toolbar

The `toolbar()` method allows you to completely override the toolbar for the field.

```php
toolbar(string|bool|array $toolbar)
```
```php
TinyMce::make('Description')
    ->toolbar('file edit view')
```

<a name="options"></a>
## Options

The `addOption()` method allows you to add additional parameters for the field.

```php
addOption(string $name, string|int|float|bool|array $value)
```
```php
TinyMce::make('Description')
    ->addOption('forced_root_block', 'div')
```
The `addCallback()` method allows you to add callback parameters for the field.

```php
addCallback(string $name, string $value)
```
```php
TinyMce::make('Description')
    ->addCallback('setup', '(editor) => console.log(editor)')
```

> [!NOTE]
> You can use strings, numbers, boolean values, and arrays as values.

<a name="file-manager"></a>
## File Manager

If you want to use the file manager in TinyMce, you need to install the [Laravel FileManager](https://github.com/UniSharp/laravel-filemanager) package.

### Installation
```php
composer require unisharp/laravel-filemanager

php artisan vendor:publish --tag=lfm_config
php artisan vendor:publish --tag=lfm_public
```

> [!NOTE]
> Be sure to set the `use_package_routes` flag in the lfm configuration to false; otherwise, route caching will result in an error.

```php
// config/lfm.php

'use_package_routes' => false,
```
### Routing
Create a routes file, for example `routes/moonshine.php`, and register the *LaravelFilemanager* routes.

```php
use Illuminate\Support\Facades\Route;
use UniSharp\LaravelFilemanager\Lfm;

Route::prefix('laravel-filemanager')->group(function () {
    Lfm::routes();
});
```

### RouteServiceProvider

Register the generated routes file in `app/Providers/RouteServiceProvider.php`.

> [!NOTE]
> The route file must be in the `moonshine` middleware group!

```php
public function boot()
{
    // ...

    $this->routes(function () {
        // ...

        Route::middleware('moonshine')
            ->namespace($this->namespace)
            ->group(base_path('routes/moonshine.php'));
    });
}
```

> [!NOTE]
> To restrict access to only users authenticated in the admin panel, you need to add the `MoonShine\Laravel\Http\Middleware\Authenticate` middleware.

```php
use MoonShine\Laravel\Http\Middleware\Authenticate;

// ...

public function boot()
{
    // ...

    $this->routes(function () {
        // ...

        Route::middleware(['moonshine', Authenticate::class])
            ->namespace($this->namespace)
            ->group(base_path('routes/moonshine.php'));
    });
}
```

### Configuration

You need to add an option for the field.

```php
TinyMce::make('Description')
    ->addOptions([
        'file_manager' => 'laravel-filemanager',
    ])
```
or add it to the configuration file `config/moonshine_tinymce.php` so that it applies to all `TinyMCe` fields.

```php
'options' => [
    'file_manager' => 'laravel-filemanager',
],
```
