# Filters

Filters are also created using [fields](/docs/{{version}}/fields/index): they are displayed only on the main page of the section.

To specify the fields to filter the data by, simply return an array with the necessary fields in the `filters()` method of your model resource.

> [!NOTE]
> If the method is absent or returns an empty array, the filters will not be displayed.

> [!NOTE]
> Some fields cannot participate in the construction of the filtering query, so they will be automatically excluded from the list of filters.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:4]
namespace App\MoonShine\Resources;

use MoonShine\UI\Fields\Text;
use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    // ...

    protected function filters(): iterable
    {
        return [
            Text::make('Title', 'title'),
        ];
    }
}
```

![filters](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/filters.png#light)
![filters_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/filters_dark.png#dark)

> [!TIP]
> Fields are a key element in building forms in **Moonshine**.
[Learn more about fields](/docs/{{version}}/fields/index).

If you need to cache the state of the filters, use the `$saveQueryState` property in the resource.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
namespace App\MoonShine\Resources;

use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    protected bool $saveQueryState = true;

    // ...
}
```
