---
title: "Helper functions"
group: "Basics"
---

Starter provides a variety of global "helper" functions. They facilitate the use of starter foundation modules and functionalities. You can reach them at any moment inside your theme components.

All helper functions should be stored in `app/helpers.php` file. Feel free to define your own functions there.

---

#### `theme()`

Helper function for accessing global Theme Service Container. Read more about usage in [Service Container]() documentation.

Calling without any parameter returns whole theme container object.

```php
use function App\Theme\theme;

$theme = theme();

// $theme: class Tonik\Gin\Foundation\Theme()
```

You can easily resolve services from the container by calling `theme($key)` function with service registration key.

```php
use function App\Theme\theme;

$config = theme('config');

// $config: class Tonik\Gin\Foundation\Config()
```

You can pass arguments to the service closure as the second parameter.

```php
theme('config', ['key' => 'value']);
```

---

#### `config()`

Alias function for resolving theme configuration defined in `config/app.php` file.

The argumentless call will give you an instance of `Tonik\Gin\Foundation\Config` class which implement the `ArrayAccess` interface, so you can iterate on it like on a standard array. Learn more in [Config documentation]().

```php
use function App\Theme\config;

$config = config();

// $config: class Tonik\Gin\Foundation\Config(['textdomain' => 'textdomain-slug'])
```

You can also resolve direct configuration values. Simply run `config` function with option key as an argument.

```php
use function App\Theme\config;

$textdomain = config('textdomain');

// $textdomain: 'textdomain-slug'
```

---

#### `template()`

Makes easy to render template parts stored in separated files. Accepts file path as the first argument and an array of values as the second argument. More detailed usage description here: [Template documentation]().

```html
<!-- @ resources/templates/partials/button.tpl.php -->
<button><?= $title ?></button>
```
```php
use function App\Theme\template;

template('partials/button', ['title' => 'Click me']);

// Outputs: <button>Click me</button>
```

You can also pass file path as an array. This allows you to render altered variants of a specific template.

```html
<!-- @ resources/templates/partials/button-input.tpl.php -->
<input type="submit" value="<?= $title ?>">
```
```php
use function App\Theme\template;

template(['partials/button', 'input'], ['title' => 'Click me']);

// Outputs: <input type="submit" value="Click me">
```

---

#### `asset()`

Returns an instance of `Tonik\Gin\Asset\Asset` class and gives you the ability to pull information like directory or URL of pulled asset. More detailed description in [Asset documentation]().

```php
use function App\Theme\asset;

$asset = asset('css/app.css');

// $asset: class Tonik\Gin\Asset\Asset()
```

---

#### `asset_path()`

Simplifies retrieving URLs of the theme's static assets.

```php
use function App\Theme\asset;

$path = asset_path('css/app.css');

// $path: '<website-address>/wp-content/themes/<theme-name>/public/css/app.css'
```

It's especially helpful while registering application stylesheets and scripts or referencing images.

```php
wp_enqueue_style('app', asset_path('css/app.css'));
```

```html
<img src="<?= asset_path('images/logotype.png') ?>">
```