---
extends: docs
title: "Adding theme supports"
group: "Basics"
subgroup: "Setup"
---

Theme supports have to be registered inside `app/Setup/supports.php` file on `after_setup_theme` action hook. Most common supports are already enabled. However, feel free to add or remove entries there.

> Take a look at [Codex](https://developer.wordpress.org/reference/functions/add_theme_support/#more-information) for all available support options.

Simply call `add_theme_support()` function with choosen option inside hooked function.

```php
namespace App\Theme\Setup;

use function App\Theme\config;

function add_theme_supports()
{
  add_theme_support('post-thumbnails');
}
add_action('after_setup_theme', 'App\Theme\Setup\add_theme_supports');
```
