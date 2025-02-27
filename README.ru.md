[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](#)

# Типография

- [Заголовок](#title)
- [Навигация](#navigations)
- [Разделитель](#divider)
- [Заголовок подраздела](#subtitle)
- [Контент](#content)
- [Пример кода](#code)
- [Списки](#list)
- [Вкладки](#tabs)
- [Уведомления](#alert)
- [Изображения](#images)

___

<a name="title"></a>
## Заголовок

Название раздела является первым и обязательным элементом страницы.

```html
# Title
```

<a name="navigations"></a>
## Навигация

Если раздел большой, то его необходимо разбить на подразделы и создать навигационное меню.

Навигационное меню представляет собой список со ссылками на подраздел. У заголовков подраздела необходимо указать якорь.

```html
- [Subtitle 1](#subtitle-1)
- [Subtitle 2](#subtitle-2)
```

> [!NOTE]
> Для разделения слов в ссылках используется `kebab-case`.

<a name="divider"></a>
## Разделитель

После навигации (содержания) необходимо указать разделитель.

```
---
```

<a name="subtitle"></a>
## Заголовок подраздела

Заголовки подразделов указываются со ссылкой, для удобного копирования ссылки на конкретный раздел документации.

```html
## Subtitle
```

Если используется [Навигация](#navigations), то необходимо перед заголовком добавить якорь:

```html
<a name="anchor"></a>
## Subtitle
```

Для названия первого пункта чаще всего необходимо использовать название `Основы`, вместо похожих `Начало`, `Введение` и др.

```html
<a name="basics"></a>
## Основы
```

Если описывается компонент, который наследуется от другого класса, и в навигации есть пункт `Основы`,
то описание наследования пишем строго после этого пункта.

```html
<a name="basics"></a>
## Основы

Наследует [Select](/docs/{{version}}/fields/select).

\* имеет те же возможности.

```

Если базовые методы описываются в другом разделе документации, то пишем так

```html
<a name="basics"></a>
## Основы

Содержит все [Базовые методы](/docs/{{version}}/fields/basic-methods).
```

<a name="content"></a>
## Контент

Кроме тегов `markdown` допускается использование `html-тегов`.

> [!WARNING]
> Все предложения должны заканчиваться точкой.

Желательно построчно синхронизировать тексты в **ru** и **en** версиях разделов.

Для выделения имени собственного используются двойные звёздочки `**`, например, `**MoonShine**`.

<a name="code"></a>
## Пример кода

- для оформления методов, классов и тд. используется одиночный апостроф ``` ` ```,
- названия методов должны заканчиваться скобками, например: `setLabel()`,
- для оформления блоков кода используется тройные апострофы ` ``` ` с указанием языка программирования и начинаться блок должен с новой строки,
- для всех классов, используемых в примерах, необходимо указать use в алфавитном порядке и обернуть их в collapse.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:1]
use MoonShine\UI\Fields\Text;

Text::make('Title')
```
или
```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:start]
use MoonShine\UI\Fields\Text; // [tl! collapse:end]

Text::make('Title')
```

Если необходимо указать какие изменения в коде, то можно воспользоваться специальной конструкцией.

```php
MenuItem::make('Settings', new SettingResource(), 'heroicons.outline.adjustments-vertical') // [tl! remove]
MenuItem::make('Settings', SettingResource::class, 'adjustments-vertical') // [tl! add]
```
или
```php
MenuItem::make('Settings', new SettingResource(), 'heroicons.outline.adjustments-vertical') // [tl! --]
MenuItem::make('Settings', SettingResource::class, 'adjustments-vertical') // [tl! ++]
```

Указать название файла или класса, к которому относится код, можно через параметр `filename`.

```
```php filename:config/moonshine.php
```

> [!WARNING]
> Использование пробелов в названиях недопустимо.

<a name="list"></a>
## Списки

```html
- элементы списка заканчивается запятой,
- после последнего элемента ставится точка.
```

<a name="tabs"></a>
## Вкладки

```
~~~tabs

tab: Tab 1
Content tab 1

tab: Tab 2
Content tab 2

~~~
```

<a name="alert"></a>
## Уведомления

В документации используется несколько типов уведомлений:

```
> [!NOTE]
> Простое уведомление.
```

```
> [!WARNING]
> Предупреждение.
```

```
> [!TIP]
> Советы.
```

<a name="images"></a>
## Изображения

Изображения добавляем в директорию `/resources/screenshots`.

Ссылку указываем - https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/filename.png

Пример:

```
![belongs_to_many](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_many.png)
```

Для показа изображения в темной или светлой теме, необходимо к ссылке добавить hash тег `#light` или `#dark`.

```
![belongs_to_many](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_many.png#light)
![belongs_to_many](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/belongs_to_many_dark.png#dark)
```
