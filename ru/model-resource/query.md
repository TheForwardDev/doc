# Запросы

- [Запросы](#query)
- [Получение записи](#receiving-a-record)
- [Eager load](#eager-load)
- [Поиск](#search)
- [Сортировка](#sorting)

---

<a name="query"></a>
## Запросы

Часто необходимо изначально изменить все запросы ресурса к базе данных.
Вы можете легко переопределить `QueryBuilder` в ресурсе.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:4]
namespace App\MoonShine\Resources;

use Illuminate\Contracts\Database\Eloquent\Builder;
use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    // ...

    protected function modifyQueryBuilder(Builder $builder): Builder
    {
        return $builder->where('active', true);
    }
}
```

> [!NOTE]
> Если вам необходимо полностью переопределить `Builder`, то вы можете переопределить метод ресурса `newQuery()`.

<a name="receiving-a-record"></a>
## Получение записи

Метод `modifyItemQueryBuilder()` используется, если вам нужно модифицировать запрос для получения записи из базы данных.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:4]
namespace App\MoonShine\Resources;

use Illuminate\Contracts\Database\Eloquent\Builder;
use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    // ...

    protected function modifyItemQueryBuilder(Builder $builder): Builder
    {
        return $builder->withTrashed();
    }
}
```

> [!NOTE]
> Если вам необходимо полностью переопределить `Builder` для получения записи, то вы можете переопределить метод ресурса `findItem()`.

<a name="eager-load"></a>
## Eager load

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
namespace App\MoonShine\Resources;

use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    protected array $with = ['user', 'categories'];

    // ...
}
```

<a name="search"></a>
## Поиск

Метод `searchQuery()` позволяет изменить запрос при поиске записей.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
namespace App\MoonShine\Resources;

use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    // ...

    protected function searchQuery(string $terms): void
    {
        return parent::searchQuery($terms)->withTrashed();
    }
}
```

Также вы можете полностью переопределить логику поиска.

```php
protected function resolveSearch(string $terms, ?iterable $fullTextColumns = null): static
{
  // Your logic

  return $this;
}
```

<a name="sorting"></a>
## Сортировка

Переопределив метод `resolveOrder()`, вы можете настроить сортировку записей.

```php
// torchlight! {"summaryCollapsedIndicator": "namespaces"}
// [tl! collapse:3]
namespace App\MoonShine\Resources;

use MoonShine\Laravel\Resources\ModelResource;

class PostResource extends ModelResource
{
    // ...

    protected function resolveOrder(string $column, string $direction, ?Closure $callback): static
    {
        if ($callback instanceof Closure) {
            $callback($this->newQuery(), $column, $direction);
        } else {
            $this->newQuery()->orderBy($column, $direction);
        }

        return $this;
    }
}
```
