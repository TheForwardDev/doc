# Url

- [Basics](#basics)
- [Title](#title)
- [Blank](#blank)

---

Inherits [Text](/docs/{{version}}/fields/text).

\* has the same capabilities.

<a name="basics"></a>
## Basics

The `Url` field is an extension of `Text` that defaults to setting `type=url`.

```php
use MoonShine\UI\Fields\Url;

Url::make('Link')
```

<a name="title"></a>
## Title

The `title()` method allows you to set the link title.

```php
title(Closure $callback)
```

```php
use MoonShine\UI\Fields\Url;

Url::make('Link')
    ->title(fn(string $url, Url $ctx) => str($url)->limit(3))
```

<a name="blank"></a>
## Blank

The `blank()` method adds the attribute `target="_blank"` for the link preview. Therefore, in this mode, the link will open in a new window.

```php
blank()
```

```php
use MoonShine\UI\Fields\Url;

Url::make('Link')
    ->blank()
```
