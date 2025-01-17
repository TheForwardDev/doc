# Import / Export
 
- [Basics](#basics)
- [Import](#import)
  - [Fields](#import-fields)
  - [Settings](#import-settings)
  - [Events](#import-events)
- [Export](#export)
  - [Fields](#export-fields)
  - [Settings](#export-settings)
- [Common methods](#methods)
- [Custom implementation](#custom)

---

<a name="basics"></a>
## Basics

To use import and export in MoonShine resources, you need to install the dependency via `composer`.

```shell
composer require moonshine/import-export
```

Next, add the `ImportExportConcern` trait and implement the `HasImportExportContract` interface.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:5]
namespace App\MoonShine\Resources;

use MoonShine\ImportExport\Contracts\HasImportExportContract;
use MoonShine\ImportExport\Traits\ImportExportConcern;
use MoonShine\Laravel\Resources\ModelResource;

class CategoryResource extends ModelResource implements HasImportExportContract
{
    use ImportExportConcern;
    
    // ...
}
```

All set! Next, just declare the fields.

<a name="import"></a>
## Import

<a name="import-fields"></a>
### Fields

To import, you need to declare the fields in the resource that will participate in the import.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use MoonShine\UI\Fields\ID;
use MoonShine\UI\Fields\Text;

protected function importFields(): iterable
  {
      return [
          ID::make(),
          Text::make('Name'),
      ];
  }
```

> [!WARNING]
> Be sure to add `ID` to the import; otherwise, records will only be added without updating existing ones.

If you need to modify a value during import, you should use the field method `fromRaw()`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
use App\Enums\StatusEnum;
use MoonShine\UI\Fields\Enum;
use MoonShine\UI\Fields\ID;

protected function importFields(): iterable
{
    return [
        ID::make(),
        Enum::make('Status')
            ->attach(StatusEnum::class)
            ->fromRaw(static fn(string $raw, Enum $ctx) => StatusEnum::tryFrom($raw)), 
    ];
}
```

<a name="import-settings"></a>
### Settings

For configuring the import, optional methods are available.
To use them, you need to add the `import()` method that returns `ImportHandler`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
use MoonShine\ImportExport\ImportHandler;
use MoonShine\Laravel\Handlers\Handler;
use MoonShine\UI\Components\ActionButton;

protected function import(): ?Handler
{
    return ImportHandler::make(__('moonshine::ui.import'))
        // Specify the IDs of users who will be notified when the operation is completed
        ->notifyUsers(fn(ImportHandler $ctx) => [auth()->id()]) 
        // Select disk
        ->disk('public') 
        // Select directory for saving the import file
        ->dir('/imports') 
        // Delete the file after import
        ->deleteAfter() 
        // CSV delimiter
        ->delimiter(',')
        // Modify button
        ->modifyButton(fn(ActionButton $btn) => $btn->class('my-class'))
  ; 
}
```

> [!NOTE]
> If the `import()` method returns `NULL`, the import button will not be displayed on the index page.

<a name="import-events"></a>
### Events

To change the import logic, you can use the model resource events.

```php
public function beforeImportFilling(array $data): array
{
    return $data;
}

public function beforeImported(mixed $item): mixed
{
    return $item;
}

public function afterImported(mixed $item): mixed
{
    return $item;
}
```

<a name="export"></a>
## Export

In the MoonShine admin panel, exporting all data considering the current filtering and sorting can be implemented.

> [!NOTE]
> By default, data is exported in `xlsx` format, but there is an option to change the format to `csv` via the `csv()` method of the `ExportHandler` class.

<a name="export-fields"></a>
### Fields

To export, you need to declare the fields in the resource that will participate in the export.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use MoonShine\UI\Fields\ID;
use MoonShine\UI\Fields\Text;

protected function exportFields(): iterable
{
    return [
        ID::make(),
        Text::make('Name'),
    ];
}
```

If you need to modify a value during export, you should use the field method `modifyRawValue()`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
use App\Enums\StatusEnum;
use MoonShine\UI\Fields\Enum;
use MoonShine\UI\Fields\ID;

protected function importFields(): iterable
{
    return [
        ID::make(),
        Enum::make('Status')
            ->attach(StatusEnum::class)
            ->modifyRawValue(static fn(StatusEnum $raw, Enum $ctx) => $raw->value), 
    ];
}
```

<a name="export-settings"></a>
### Settings

For configuring the export, optional methods are available.
To use them, you need to add the `export()` method that returns `ExportHandler`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
use MoonShine\ImportExport\ExportHandler;
use MoonShine\Laravel\Handlers\Handler;
use MoonShine\UI\Components\ActionButton;

protected function export(): ?Handler
{
    return ExportHandler::make(__('moonshine::ui.export'))
        // Specify the IDs of users who will be notified when the operation is completed
        ->notifyUsers(fn() => [auth()->id()]) 
        // Select disk
        ->disk('public') 
        // Filename
        ->filename(sprintf('export_%s', date('Ymd-His'))) 
        // Select directory for saving the export file
        ->dir('/exports') 
        // If you need to export in csv format
        ->csv() 
        // CSV delimiter
        ->delimiter(',') 
        // Export with confirmation
        ->withConfirm()
        // Modify button
        ->modifyButton(fn(ActionButton $btn) => $btn->class('my-class'))
  ; 
}
```

> [!NOTE]
> If the `export()` method returns `NULL`, the export button will not be displayed on the index page.

<a name="methods"></a>
## Common methods

`ImportHandler` and `ExportHandler` extend the base class `Handler`, which implements additional methods.

#### icon

```php
// icon for the button
icon(string $icon)
```

#### queue

```php
// run processes in the background
queue()
```

#### modifyButton

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:1]
use MoonShine\UI\Components\ActionButton;
 
// modify button
modifyButton(fn(ActionButton $btn) => $btn->class('my-class'))
```

#### notifyUsers

```php
// select users for notification
notifyUsers(fn() => [auth()->id()]) 
```

#### when

```php
// methods by condition
when($value = null, callable $callback = null, callable $default = null)
```

`$value` - condition,  
`$callback` - `callback` function that will be executed if the condition is `TRUE`, 
`$default` - `callback` function that will be executed if the condition is `FALSE`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use MoonShine\ImportExport\ImportHandler;
use MoonShine\Laravel\Handlers\Handler;

protected function import(): ?Handler
{
    return ImportHandler::make('Import')
        ->when(
            true,
            fn($handler) => $handler->delimiter(','),
            fn($handler) => $handler->delimiter(';')
        );
}
```

#### unless

```php
// methods by condition
unless($value = null, callable $callback = null, callable $default = null)
```

`$value` - condition,  
`$callback` - `callback` function that will be executed if the condition is `FALSE`,
`$default` - `callback` function that will be executed if the condition is `TRUE`.

> [!NOTE]
> The `unless()` method is the reverse of the `when()` method.

<a name="custom"></a>
## Custom implementation

There may be situations where you want to change the import or export implementation. To do this, you need to implement your own class extending `ImportHandler` or `ExportHandler`.

You can generate the class by using the console command:

```shell
php artisan moonshine:handler
```

After running the command, a base class `Handler` will be created in the `app/MoonShine/Handlers` directory.

> [!NOTE]
> Don’t forget to change the inheritance from `Handler` to `ImportHandler` or `ExportHandler`.
