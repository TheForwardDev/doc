# TinyMce

- [Установка](#installation)
- [Основы](#basics)
- [Конфиг по умолчанию](#default-config)
- [Язык](#locale)
- [Plugins](#plugins)
- [Menubar](#menubar)
- [Панель инструментов](#toolbar)
- [Опции](#options)
- [Файловый менеджер](#file-manager)

---

Наследует [Textarea](/docs/{{version}}/fields/textarea).

* имеет те же возможности

> [!WARNING]
> Прежде чем использовать это поле, вы должны зарегистрироваться на сайте [Tiny.Cloud](https://www.tiny.cloud), получить токен и добавить его в `.env`.

```
TINYMCE_TOKEN="YOUR_TOKEN"
```

---

<a name="installation"></a>
## Установка

```shell
composer require moonshine/tinymce
```

<a name="basics"></a>
## Основы

```php
use MoonShine\TinyMce\Fields\TinyMce;

TinyMce::make('Description')
```

<a name="default-config"></a>
## Конфиг по умолчанию

Поле `TinyMce` по умолчанию использует наиболее распространенные настройки, такие как плагины, панель меню и панель инструментов.

Чтобы изменить настройки по умолчанию, вам необходимо опубликовать файл конфигурации:

```php
php artisan vendor:publish --tag="moonshine-tinymce-config"
```

Вы также можете добавить дополнительные параметры в файл конфигурации, которые будут применяться ко всем полям `TinyMce`.

```php
'options' => [
    'forced_root_block' => 'div',
    'force_br_newlines' => true,
    'force_p_newlines' => false,
],
```

<a name="locale"></a>
## Язык

По умолчанию используется локаль вашего приложения, но с помощью метода `locale()` вы можете определить конкретную локаль.

```php
locale(string $locale)
```
```php
TinyMce::make('Description')
    ->locale('ru');
```

В настоящее время доступны английский (en), русский (ru) и украинский (uk), но мы всегда готовы добавить остальные.

Чтобы добавить новые локализации, создайте задачу или отправьте запрос на включение

<a name="plugins"></a>
## Plugins

Метод `plugins()` позволяет вам полностью переопределить плагины, которые будут использовать поле.

```php
plugins(array $plugins)
```
```php
TinyMce::make('Description')
    ->plugins(['code', 'image', 'link', 'media', 'table'])
```

Метод `addPlugins()` позволяет добавлять новые плагины к плагинам по умолчанию.

```php
addPlugins(array $plugins)
```
```php
TinyMce::make('Description')
    ->addPlugins(['wordcount'])
```

Метод `removePlugins()` позволяет исключить плагины, которые будут использоваться в поле.

```php
removePlugins(array $plugins)
```
```php
TinyMce::make('Description')
    ->removePlugins(['autoresize'])
```

<a name="menubar"></a>
## Menubar

Метод `menubar()` позволяет полностью переопределить строку меню для поля.

```php
menubar(string|bool $menubar)
```
```php
TinyMce::make('Description')
    ->menubar('file edit view')
```

<a name="toolbar"></a>
## Toolbar

Метод `toolbar()` позволяет полностью переопределить панель инструментов для поля.

```php
toolbar(string|bool|array $toolbar)
```
```php
TinyMce::make('Description')
    ->toolbar('file edit view')
```

<a name="options"></a>
## Опции

Метод `addOption()` позволяет добавлять дополнительные параметры для поля.

```php
addOption(string $name, string|int|float|bool|array $value)
```
```php
TinyMce::make('Description')
    ->addOption('forced_root_block', 'div')

```
Метод `addCallback()` позволяет вам добавлять параметры обратного вызова для поля.

```php
addCallback(string $name, string $value)
```
```php
TinyMce::make('Description')
    ->addCallback('setup', '(editor) => console.log(editor)')
```

> [!NOTE]
> В качестве значений можно использовать строку, число, логическое значение и массив.

<a name="file-manager"></a>
## Файловый менеджер

Если вы хотите использовать файловый менеджер в TinyMce, вам необходимо установить пакет [Laravel FileManager](https://github.com/UniSharp/laravel-filemanager).

### Установка
```php
composer require unisharp/laravel-filemanager

php artisan vendor:publish --tag=lfm_config
php artisan vendor:publish --tag=lfm_public
```

> [!NOTE]
> Обязательно установите для флага use_package_routes в конфигурации lfm значение false, иначе кеширование маршрутов приведет к ошибке.

```php
// config/lfm.php

'use_package_routes' => false,
```
### Маршрутизация
Создайте файл маршрутов, например `«`routes/moonshine.php`, и зарегистрируйте маршруты *LaravelFilemanager*.

```php
use Illuminate\Support\Facades\Route;
use UniSharp\LaravelFilemanager\Lfm;

Route::prefix('laravel-filemanager')->group(function () {
    Lfm::routes();
});
```

### RouteServiceProvider

Зарегистрируйте сгенерированный файл маршрутов в `app/Providers/RouteServiceProvider.php`

> [!NOTE]
> Файл маршрута должен находиться в группе `moonshine` промежуточного программного обеспечения!

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
> Чтобы разрешить доступ только пользователям, авторизованным в админ-панели, вам необходимо добавить промежуточное программное обеспечение `MoonShine\Laravel\Http\Middleware\Authenticate`.

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

### Конфигурация

Вам нужно добавить опцию для поля

```php
TinyMce::make('Description')
    ->addOptions([
        'file_manager' => 'laravel-filemanager',
    ])
```
или добавьте в файл конфигурации `config/moonshine_tinymce.php`, чтобы он применялся ко всем полям `TinyMCe`.

```php
'options' => [
    'file_manager' => 'laravel-filemanager',
],
```
