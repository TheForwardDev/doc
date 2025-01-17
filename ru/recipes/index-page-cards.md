# Индексная страница через CardsBuilder

Давайте изменим отображение элементов на индексной странице через компонент *CardsBuilder*.

```php
class MoonShineUserResource extends ModelResource
{
    // ...

    public function getListEventName(?string $name = null, array $params = []): string
    {
        $name ??= $this->getListComponentName();

        return AlpineJs::event(JsEvent::CARDS_UPDATED, $name, $params);
    }

    public function modifyListComponent(ComponentContract $component): ComponentContract
    {
        return CardsBuilder::make($this->getItems(), $this->getIndexFields())
            ->cast($this->getCaster())
            ->name($this->getListComponentName())
            ->async()
            ->overlay()
            ->title('email')
            ->subtitle('name')
            ->url(fn ($user) => $this->getFormPageUrl($user->getKey()))
            ->thumbnail(fn ($user) => asset($user->avatar))
            ->buttons($this->getIndexButtons());
    }

    // ...
}
```
