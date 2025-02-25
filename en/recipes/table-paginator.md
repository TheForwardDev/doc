# Paginator

Paginator for *TableBuilder*

```php
protected function components(): iterable
{
    $posts = Post::query()->paginate();

    $paginator = (new PaginatorCaster(
        $posts->appends(request()->except('page'))->toArray(),
        $posts->items()
    ))->cast();

    return [
        TableBuilder::make()
            ->fields([
                Text::make('Name')
            ])
            ->items($paginator)
    ];
}
```
