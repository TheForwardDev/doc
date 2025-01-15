# Events

Since **MoonShine** is based on the standard **Eloquent** methods for adding, editing, and deleting, you can easily utilize the standard [events](https://laravel.com/docs/eloquent#events) of **Laravel**.

However, there is also a need to specifically bind to events within the **MoonShine** resources!
To do this, you need to implement the required events in your resource.

```php
protected function beforeCreating(mixed $item): mixed
{
    if (auth()->user()->moonshine_user_role_id !== 1) {
        request()->merge([
            'author_id' => auth()->id(),
        ]);
    }

    return $item;
}

protected function afterCreated(mixed $item): mixed
{
    return $item;
}

protected function beforeUpdating(mixed $item): mixed
{
    if (auth()->user()->moonshine_user_role_id !== 1) {
        request()->merge([
            'author_id' => auth()->id(),
        ]);
    }

    return $item;
}

protected function afterUpdated(mixed $item): mixed
{
    return $item;
}

protected function beforeDeleting(mixed $item): mixed
{
    return $item;
}

protected function afterDeleted(mixed $item): mixed
{
    return $item;
}

protected function beforeMassDeleting(array $ids): void
{
    // Logic goes here
}

protected function afterMassDeleted(array $ids): void
{
    // Logic goes here
}
```
