# Markdown

- [Installation](#installation)
- [Basics](#basics)
- [Default Config](#default-config)
- [Toolbar](#toolbar)
- [Options](#options)

---

> [!NOTE]
> More information about the field can be found in the [repository](https://github.com/moonshine-software/easymde).

> [!NOTE]
> Based on the [EasyMDE](https://github.com/Ionaru/easy-markdown-editor) library.

<a name="installation"></a>
## Installation

To use the field, you need to install the package:

```shell
composer require moonshine/easymde
```

<a name="basics"></a>
## Basics

Inherits from [Textarea](/docs/{{version}}/fields/textarea).

\* has the same capabilities.

```php
use MoonShine\EasyMde\Fields\Markdown;

Markdown::make('Description')
```

<a name="default-config"></a>
## Default Config

The `Markdown` field by default uses the most common settings, such as plugins, menu panel, and toolbar.

To change the default settings, you need to publish the configuration file:

```shell
php artisan vendor:publish --tag="moonshine-easymde-config"
```

You can also add additional parameters to the configuration file that will apply to all `Markdown` fields.

```php
return [
    'previewClass' => ['prose', 'dark:prose-invert'],
    'forceSync' => true,
    'spellChecker' => false,
    'status' => false,
    'toolbar' => [
        'bold', 'italic', 'strikethrough', 'code', 'quote', 'horizontal-rule', '|', 'heading-1',
        'heading-2', 'heading-3', '|', 'table', 'unordered-list', 'ordered-list', '|', 'link', 'image', '|',
        'preview', 'side-by-side', 'fullscreen', '|', 'guide',
    ],
];
```

<a name="toolbar"></a>
## Toolbar

The `toolbar()` method allows you to completely override the toolbar for the field.

```php
toolbar(string|bool|array $toolbar)
```

```php
Markdown::make('Description')
    ->toolbar(['bold', 'italic', 'strikethrough', 'code', 'quote', 'horizontal-rule'])
```

<a name="options"></a>
## Options

The `addOption()` method allows you to add additional parameters for the field.

```php
addOption(string $name, string|int|float|bool|array $value)
```

```php
Markdown::make('Description')
    ->addOption('toolbar', ['bold', 'italic', 'strikethrough', 'code', 'quote', 'horizontal-rule'])
```
