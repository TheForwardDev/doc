# MobileBar

> [!NOTE]
> Используется для создания [шаблонов](/docs/{{version}}/appearance/layout) в **MoonShine**.

Компонент `MobileBar` необходим если вы хотите кастомизировать мобильную выпадающую панель по своему,
так как по умолчанию дублируется содержимое `TopBar` или `Sidebar`.

```php
make(iterable $components = [])
```

- `$components` - массив компонентов.

```php
use MoonShine\UI\Components\Layout\MobileBar;

MobileBar::make([
    Div::make([
        Div::make([
            $this->getLogoComponent(),
        ])->class('menu-heading-logo'),

        Div::make([
            ThemeSwitcher::make(),

            Div::make([
                Burger::make(),
            ])->class('menu-heading-burger'),
        ])->class('menu-heading-actions'),
    ])->class('menu-heading'),

    Div::make([
        Menu::make(),
        When::make(
            fn (): bool => $this->isAuthEnabled(),
            static fn (): array => [Profile::make(withBorder: true)],
        ),
    ])->customAttributes([
        'class' => 'menu',
        ':class' => "asideMenuOpen && '_is-opened'",
    ]),
])
```
