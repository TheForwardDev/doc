# Code

- [Installation](#installation)
- [Basics](#basics)
- [Default Config](#default-config)
- [Language](#language)
- [Themes](#themes)
- [Options](#options)

---

> [!NOTE]
> More information about the field can be found in the [package repository](https://github.com/moonshine-software/ace).

<a name="installation"></a>
## Installation

Before using, you need to install the package:

```bash
composer require moonshine/ace
```

<a name="basics"></a>
## Basics

Inherits [Textarea](/docs/{{version}}/fields/textarea).

\* has the same capabilities.

The Code field is an extension of *Textarea* with a visual layout for editing code.

```php
use MoonShine\Ace\Fields\Code;

Code::make('Code')
```

![fields_code](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/code.png)

> [!NOTE]
> The field is based on the [Ace](https://ace.c9.io/) library.


<a name="default-config"></a>
## Default Config

To change the default settings, you need to publish the configuration file:

```bash
php artisan vendor:publish --tag="moonshine-ace-config"
```

You can also add additional parameters to the configuration file that will apply to all `Code` fields.

```php
'options' => [
    'language' => 'javascript',
    'options' => [
        'useSoftTabs' => true,
        'navigateWithinSoftTabs' => true,
    ],
    'themes' => [
        'light' => 'chrome',
        'dark' => 'cobalt'
    ],
],
```

<a name="language"></a>
## Language

By default, the layout for PHP is used, but you can change it for another programming language using the `language()` method.

```php
language(string $language)
```

Supported languages: *HTML*, *XML*, *CSS*, *PHP*, *JavaScript*, and many others.

```php
Code::make('Code')
    ->language('js')
```

<a name="themes"></a>
## Themes

To change themes, use the `themes()` method.

```php
themes(string $light = null, string $dark = null)
```

```php
Code::make('Code')
    ->themes('chrome', 'cobalt');
```

<a name="options"></a>
## Options

The `addOption()` method allows you to add additional options for the field.

```php
addOption(string $name, string|int|float|bool $value)
```

```php
Code::make('Code')
    ->addOption('showGutter', false)
```
