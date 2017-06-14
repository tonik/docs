---
extends: docs
title: "Asset"
group: "Architecture"
prev: config
next: integrating-advanced-custom-fields
order: 1
---

The `Tonik\Gin\Asset\Asset` class provides simple API for retrieving information and details about theme asset files. You can easily pull they URLs, directory paths or check if actually exist.

## Usage

#### Initializing asset

Asset requires the `Tonik\Gin\Foundation\Config` class to be injected with `paths` and `directories` properties set up.

```php
use Tonik\Gin\Asset\Asset;
use Tonik\Gin\Foundation\Config;

$config = new Config([
  'paths' => [
    'directory' => get_template_directory(),
    'uri' => get_template_directory_uri(),
  ],
  'directories' => [
    'assets' => 'resources/assets',
    'public' => 'public',
  ]
]);

$asset = new Asset($config);
```

Now, you can set a path to the file you are looking for. This path should be relative to the `public` directory.

```php
$asset->setFile('js/app.js');
```

#### Getting asset relative path

Gets asset path relatively to the project root directory.

```php
$asset->getRelativePath();

// 'public/js/app.js'
```

#### Getting asset URI

Gets URI to the asset on your server.

```php
$asset->getUri();

// 'http://website.com/wp-content/themes/<theme-name>/public/js/app.js'
```

#### Getting asset path

Gets full directory path to the asset on your server.

```php
$asset->getPath();

// 'website/directory/wp-content/themes/<theme-name>/public/js/app.js'
```

#### Checking if asset file exist

You can check if asset file actually exists with `fileExist` method.

```php
$asset->fileExists();

// true or false
```
