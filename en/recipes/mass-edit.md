# Bulk editing of rows

In this example, we will add a `bulk` button to the `indexButtons` list and edit the titles of all entries in the modal window.

The example uses the system **MoonShineUserRoleResource**:

> [!NOTE]
> If you decide to use this recipe, be sure to add validation and use the example wisely

```php
public function massEdit(MoonShineRequest $request): MoonShineJsonResponse
{
    MoonshineUserRole::query()
        ->whereIn('id', $request->array('ids'))
        ->update([
            'name' => $request->input('name')
        ]);

    return MoonShineJsonResponse::make()->toast('Success', ToastType::SUCCESS);
}

protected function indexButtons(): ListOf
{
    return parent::indexButtons()->add(
        ActionButton::make('')
            ->bulk()
            ->icon('pencil')
            ->inModal(
                'Mass edit',
                fn() => FormBuilder::make()
                    ->name('mass-edit')
                    ->fields([
                        HiddenIds::make($this->getListComponentName()),
                        Text::make('Name')->required(),
                    ])
                    ->asyncMethod('massEdit', events: [
                        AlpineJs::event(JsEvent::TABLE_UPDATED, $this->getListComponentName())
                    ])
                    ->submit('Save'),
            ),
    );
}
```
