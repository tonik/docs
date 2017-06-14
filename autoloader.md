---
extends: docs
title: "Autoloader"
group: "Architecture"
prev: template
next: theme-service-container
order: 4
---

The `Tonik\Gin\Foundation\Autoloader` class helps with autoloading theme components files.

## Usage

### Initializing autoloader

Autoloader class requires instance of `Tonik\Gin\Foundation\Config` to be injected with setup `paths`, `directories` and `autoload` properties. The `autoload` option should include list of component relative to the `app/` directory paths.

```php
use Tonik\Gin\Foundation\Config;
use Tonik\Gin\Foundation\Autoloader;

$config = new Config([
  'paths' => [
    'directory' => get_template_directory(),
  ],
  'directories' => [
    'app' => 'app',
  ],
  'autoload' => [
    'Http/assets.php',
  ]
]);

$autoloader = new Autoloader($config);
```

### Requiring components listed to autoload

To autoload listed component simply call `load` method. This will `require_once` all listed files.

```php
$autoloader->load();
```

### Getting relative path of autoloaded component

Gets path of a specified component relatively to the project `app` directory.

```php
$autoloader->getRelativePath('Http/assets.php');

// 'app/Http/assets.php'
```

### Getting path of autoloaded component

Gets full directory path to the component file on your server.

```php
$autoloader->getPath('Http/assets.php');

// 'website/directory/app/Http/assets.php'
```

## Actions

#### `tonik/gin/autoloader/before_load`

Fires before requiring listed files by autoloader.

```php
add_action('tonik/gin/autoloader/before_load', function() {
  // logic
});
```

#### `tonik/gin/autoloader/after_load`

Fires after requiring listed files by autoloader.

```php
add_action('tonik/gin/autoloader/after_load', function() {
  // logic
});
```
