# Changing Breadcrumbs from Resource

You can change the breadcrumbs of a page directly from the resource.

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
