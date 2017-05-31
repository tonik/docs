---
extends: _layouts.docs
title: "Theme Service Container"
group: "Architecture"
---

The `Tonik\Gin\Foundation\Theme` class is a backbone of the theme which performs the services container role. It utilizes a [singleton pattern](//en.wikipedia.org/wiki/Singleton_pattern), so every time you initiate it you will receive the same object.

## Usage

### Initializing theme container

```php
use Tonik\Gin\Foundation\Theme;

$theme = new Theme;
```

### Binding services in the container

To bind a value inside container simply call `bind` or `factory` method with a binding name as the first parameter. The second argument should be a closure which returns desired value.

```php
$theme->bind('basic', function() {
    return 'value';
});
```

Inside closure callback, you have access to the two parameters. First is an instance of `Tonik\Gin\Foundation\Theme`, second are variables passed on service resolving.

```php
$theme->bind('basic/parameters', function(Theme $theme, $parameters) {
    // $theme: class Tonik\Gin\Foundation\Theme
    // $parameters: ['key' => 'value']
});

// Resolve service with parameter.
$theme->get('basic/parameters', ['key' => 'value']);
```

#### Binding singletons

Use `bind` method to create singleton service. You will receive the same instance of service every time you resolve it from the container.

```php
use Tonik\Gin\Foundation\Config;

$theme->bind('singleton', function() {
    return new Config(['option' => 'value']);
});
```

#### Binding factories

The `factory` method allows you to create service which returns you a new instance on every resolving.

```php
$theme->factory('service', function () {
    return new Config(['option' => 'value']);
});
```

### Resolving services from the container

Run `get` method with service name as an argument to resolve previously bounded value out of the container.

```php
$theme->get('service');
```

You can also resolve services which are requiring some sort of parameter.

```php
$theme->get('basic/parameters', ['key' => 'value']);
```

### Checking for bonded service

You may want to check if service is already bounded inside the container. Use `has` method and service name as a parameter.

```php
$theme->has('service');
```

### Removing service from the container

Call `forget` to remove previously bounded service inside the container.

```php
$theme->forget('service');
```