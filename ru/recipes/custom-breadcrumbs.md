# Изменение хлебных крошек из ресурса

Вы можете изменить хлебные крошки страницы непосредственно из ресурса.

```php
class MoonShineUserResource extends ModelResource
{
    // ...

    protected function onLoad(): void
    {
        parent::onLoad();

        $this->getFormPage()->breadcrumbs([
            '/custom' => 'Custom',
            '#' => $this->getTitle(),
        ]);
    }

    // ...
}
```
