# Password

- [Basics](#basics)
- [PasswordRepeat](#password-repeat)

---

<a name="basics"></a>
## Basics

Inherits from [Text](/docs/{{version}}/fields/text).

\* has the same capabilities.

The *Password* and *PasswordRepeat* fields are intended for working with passwords, and they are by default set to `type=password`.

The *Password* field displays as `***` in preview mode, and when the `apply()` method is executed, the field value is encoded using the `make` method of the class bound to the `Illuminate\Contracts\Hashing\Hasher` interface.

> [!NOTE]
> In **Laravel**, by default, the Hasher class is the facade `Illuminate\Support\Facades\Hash`.

```php
use MoonShine\UI\Fields\Password;

Password::make('Password')
```

<a name="password-repeat"></a>
## PasswordRepeat

*PasswordRepeat* inherits from *Password* and is used as a helper field for confirming the password, and it does not alter the data when the `apply()` method is executed.

```php
use MoonShine\UI\Fields\Password;
use MoonShine\UI\Fields\PasswordRepeat;

Password::make('Password'),
PasswordRepeat::make('Password repeat', 'password_repeat')
```
