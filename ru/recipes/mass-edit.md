# Массовое редактирование записей

В данным примере мы добавим `bulk` кнопку в список `indexButtons` и в модальном окне отредактируем заголовки всех записей.

В примере используется системный **MoonShineUserRoleResource**:

> [!NOTE]
> Если решите использовать данный рецепт, не забудьте добавить валидацию и используйте пример с умом

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
