# HasOne

- [Основы](#basics)
- [Поля](#fields)
- [ID родителя](#parent-id)
- [Модификация](#modify)

---

<a name="basics"></a>
## Основы

Поле `HasOne` предназначено для работы с одноименной связью в **Laravel** и включает все [Базовые методы](/docs/{{version}}/fields/basic-methods).

```php
HasOne::make(
    Closure|string $label,
    ?string $relationName = null,
    Closure|string|null $formatted = null,
    ModelResource|string|null $resource = null,
)
```

- `$label` - метка, заголовок поля,
- `$relationName` - имя отношения,
- `$resource` - `ModelResource`, на который ссылается отношение.

> [!WARNING]
> Параметр `$formatted` не используется в поле `HasOne`!

> [!WARNING]
> Наличие `ModelResource`, на который ссылается отношение, обязательно.
> Ресурс также необходимо [зарегистрировать](/docs/{{version}}/model-resource/index#declaring-in-the-system) в сервис-провайдере `MoonShineServiceProvider` в методе `$core->resources()`.
> В противном случае будет ошибка 500.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use App\MoonShine\Resources\ProfileResource;
use MoonShine\Laravel\Fields\Relationships\HasOne;

HasOne::make(
    'Profile',
    'profile',
    resource: ProfileResource::class
)
```

![has_one](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one.png#light)
![has_one_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one_dark.png#dark)

Если вы не указываете `$relationName`, тогда имя отношения будет определено автоматически на основе `$label` (по правилам camelCase).

```php
use MoonShine\Laravel\Fields\Relationships\HasOne;

HasOne::make('Profile', 'profile')
```

Вы можете опустить `$resource`, если `ModelResource` совпадает с названием связи.

```php
use MoonShine\Laravel\Fields\Relationships\HasOne;

HasOne::make('Profile')
```

<a name="fields"></a>
## Поля

Метод `fields()` позволяет указать, какие поля будут участвовать в *preview* или в построении форм.

```php
fields(FieldsContract|Closure|iterable $fields)
```

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:4]
use App\MoonShine\Resources\ProfileResource;
use MoonShine\UI\Fields\Relationships\HasOne;
use MoonShine\UI\Fields\Phone;
use MoonShine\UI\Fields\Text;

HasOne::make('Profile', resource: ProfileResource::class)
    ->fields([
        Phone::make('Phone'),
        Text::make('Address'),
    ])
```

![has_one_preview](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one_preview.png#light)
![has_one_preview_dark](https://raw.githubusercontent.com/moonshine-software/doc/3.x/resources/screenshots/has_one_preview_dark.png#dark)

<a name="parent-id"></a>
## ID родителя

Если у отношения есть ресурс, и вы хотите получить ID родительского элемента, то вы можете использовать трейт `ResourceWithParent`.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use MoonShine\Laravel\Resources\ModelResource;
use MoonShine\Traits\Resource\ResourceWithParent;

class PostImageResource extends ModelResource
{
    use ResourceWithParent;

    // ...
}
```

При использовании трейта необходимо определить методы:

```php
protected function getParentResourceClassName(): string
{
    return PostResource::class;
}

protected function getParentRelationName(): string
{
    return 'post';
}
```

Для получения ID родителя используйте метод `getParentId()`.

```php
$this->getParentId();
```

<a name="modify"></a>
## Модификация

### Preview

Метод `modifyTable()` позволяет изменить `TableBuilder` для предпросмотра.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
use App\MoonShine\Resources\CommentResource;
use MoonShine\Laravel\Fields\Relationships\HasOne;
use MoonShine\UI\Components\Table\TableBuilder;

HasOne::make('Comment', resource: CommentResource::class)
    ->modifyTable(
        fn(TableBuilder $table) => $table
    )
```

### Форма

Метод `modifyForm()` позволяет изменить `FormBuilder` для редактирования.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
use App\MoonShine\Resources\CommentResource;
use MoonShine\UI\Components\FormBuilder;
use MoonShine\Laravel\Fields\Relationships\HasOne;

HasOne::make('Comment', resource: CommentResource::class)
    ->modifyForm(
        fn(FormBuilder $form) => $form->submit('Custom title')
    )
```

### Редирект после изменения

Метод `redirectAfter()` позволяет редирект после сохранения/добавления/удаления.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:2]
use App\MoonShine\Resources\CommentResource;
use MoonShine\Laravel\Fields\Relationships\HasOne;

HasOne::make('Comment', resource: CommentResource::class)
    ->redirectAfter(fn(int $parentId) => route('home'))
```
