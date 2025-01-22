# StackFields

- [Basics](#basics)
- [Edit View](#edit-view)
- [Conditional Display](#view-condition)

---

<a name="basics"></a>
## Basics

The `StackFields` field allows you to group fields when displaying in the preview.

The `fields()` method should accept an array of fields to group.

```php
use MoonShine\Laravel\Fields\BelongsTo;
use MoonShine\UI\Fields\StackFields;
use MoonShine\UI\Fields\Text;

StackFields::make('Title')->fields([
    Text::make('Title'),
    BelongsTo::make('Author', resource: 'name'),
])
```

<a name="edit-view"></a>
## Edit View

You can customize the display for `StackFields` using components:

```php
StackFields::make('Title')->fields([
    Text::make('Title'),
    LineBreak::make(), // adds a line break
    BelongsTo::make('Author', resource: 'name'),
])
```

<a name="view-condition"></a>
## Conditional Display

To change the set of components in `StackFields` under certain conditions, you need to pass a condition and sets of components using a callback function.

```php
StackFields::make('Stack')->fields(fn(StackFields $ctx) => $ctx->getData()?->getOriginal()->id === 3 ? [
    Date::make(__('moonshine::ui.resource.created_at'), 'created_at')
        ->format("d.m.Y")
        ->sortable(),
] : [
    Date::make(__('moonshine::ui.resource.created_at'), 'created_at')
        ->format("d.m.Y")
        ->sortable(),
    LineBreak::make(),
    Email::make(__('moonshine::ui.resource.email'), 'email')
        ->sortable(),
])
```
