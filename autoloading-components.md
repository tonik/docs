---
extends: docs
title: "Autoloading components"
group: "Basics"
subgroup: "General"
---

Dividing code into files improves project organization and readability. However, requiring all these files manually can be tough and make a mess really fast. In order to make it easier, the starter brings simple loading system for theme's components files. It uses `localize_template()` under the hood and supports child theme overriding.

Registered files are autoloaded on theme bootstrap in `functions.php` file.

## Configuration

You can register components in the `config/app.php` configuration file with `autoload` option. It holds a list of file paths which will be autoloaded. Remember, order on the list matters, paths should be entered as relative to the `app/` directory.

> Note! Make sure that `helpers.php` file is registered first. All other components usually make use of helper functions inside.

```php
'autoload' => [
    'helpers.php',
    'Structure/navs.php',
    'Structure/widgets.php',
    'Structure/sidebars.php',
    'Structure/posttypes.php',
    'Structure/taxonomies.php',
    'Structure/shortcodes.php',
    'Structure/thumbnails.php',
    'Setup/actions.php',
    'Setup/filters.php',
    'Setup/supports.php',
    'Setup/services.php',
    'Http/assets.php',
    'Http/ajaxes.php',
]
```

## Usage

> Visit [Autoloader]() guide if you looking for API documentation.

In order to autoload your own new component, add a new entry to the `autoload` list. For example, you created `app/Structure/settings.php` file, so to autoload it enter `Structure/settings.php` path to the list.

```php
'autoload' => [
    //...
    'Structure/settings.php',
    //...
]
```
