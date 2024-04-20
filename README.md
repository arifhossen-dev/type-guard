<p align="center">
    <img src="https://raw.githubusercontent.com/pinkary-project/type-guard/master/docs/example.jpg" height="300" alt="Logo of Pinkary Project">
    <p align="center">
        <a href="https://github.com/pinkary-project/type-guard/actions"><img alt="GitHub Workflow Status (master)" src="https://github.com/pinkary-project/type-guard/actions/workflows/tests.yml/badge.svg"></a>
        <a href="https://packagist.org/packages/pinkary-project/type-guard"><img alt="Total Downloads" src="https://img.shields.io/packagist/dt/pinkary-project/type-guard"></a>
        <a href="https://packagist.org/packages/pinkary-project/type-guard"><img alt="Latest Version" src="https://img.shields.io/packagist/v/pinkary-project/type-guard"></a>
        <a href="https://packagist.org/packages/pinkary-project/type-guard"><img alt="License" src="https://img.shields.io/packagist/l/pinkary-project/type-guard"></a>
    </p>
</p>

------

> This library is a **work in progress**. Please, do not use it in production.

Type Guard module is part of the [Pinkary Project](https://github.com/pinkary-project), and allows you to **narrow down the type** of a variable to a more specific type.  Using the `type` function, you can perform specific checks to determine the type of an object and then use that object in a way that is **type-safe** according to the [PHPStan](https://phpstan.org/) and [Psalm](https://psalm.dev/) static analyzers.

Here is an example, where we use the `type` function to narrow down the type of a variable that previously had a `mixed` type:

```php
function config(): mixed;

// At compile time, the type of $apiKey is `mixed`:
$apiKey = config('api_key');

// We instruct the static analyzer that $apiKey is a `string`:
$apiKey = type($apiKey)->asString();
```

Here is another example, where we use the `type` function to narrow down the type of a variable that previously could be `null`. In the process, zero type information is lost:

```php
/** @var array<int, User>|null $users */
$users = getUsers();

// Narrows down the type to `array<int, User>`
$users = type($users)->not()->null();
```

And one more example, where we narrow down the type of a variable to a Collection without losing the type information:

```php
/** @var Collection<int, User>|null $users */
$users = getUsers();

// Narrows down the type to `Collection<int, User>`
$users = type($users)->as(Collection::class);
```

## Installation

> **Requires [PHP 8.2+](https://php.net/releases/)**

You may use [Composer](https://getcomposer.org) to install Type Guard into your PHP project:

```bash
composer require pinkary-project/type-guard
```

## Usage

- [`as`](#as)
- [`asInt()`](#asint)
- [`asFloat()`](#asfloat)
- [`asString()`](#asstring)
- [`asBool()`](#asbool)
- [`asNull()`](#asnull)
- [`asCallable()`](#ascallable)
- [`not()->null()`](#notnull)
- [`asArray()`](#asarray)
- [`asIterable()`](#asiterable)

### `as`

Asserts and narrows down the type of the given variable to a more specific type.

```php
$variable = type($variable)->as(User::class);
```

### `asInt()`

Asserts and narrows down the type of the given variable to an integer.

```php
$variable = type($variable)->asInt();
```

### `asFloat()`

Asserts and narrows down the type of the given variable to a float.

```php
$variable = type($variable)->asFloat();
```

### `asString()`

Asserts and narrows down the type of the given variable to a string.

```php
$variable = type($variable)->asString();
```

### `asBool()`

Asserts and narrows down the type of the given variable to a boolean.

```php
$variable = type($variable)->asBool();
```

### `asNull()`

Asserts and narrows down the type of the given variable to a null.

```php
$variable = type($variable)->asNull();
```

### `asCallable()`

Asserts and narrows down the type of the given variable to a callable.

```php
$variable = type($variable)->asCallable();
```

### `not()->null()`

Asserts and narrows down the type of the given variable to a non-null value.

```php
$variable = type($variable)->not()->null();
```

### `asArray()`

Asserts and narrows down the type of the given variable to an array.

```php
$variable = type($variable)->asArray();
```
### `asIterable()`

Asserts and narrows down the type of the given variable to an iterable.

```php
$variable = type($variable)->asIterable();
```


------

**Type Guard** is part of the [Pinkary Project](https://github.com/pinkary-project) project. It was created by **[Nuno Maduro](https://twitter.com/enunomaduro)** and open-sourced under the **[MIT license](https://opensource.org/licenses/MIT)**.
