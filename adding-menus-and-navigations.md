---
extends: docs
title: "Adding menus and navigations"
group: "Basics"
subgroup: "Structure"
prev: registering-custom-taxonomies
next: adding-thumbnail-sizes
order: 3
---

Navigations allow for creating easily customizable menus areas, which can be managed inside "Appearance > Menus" administration panel.

You should register navigations in `app/Structure/navs.php` file with `register_nav_menus` function. By default, starter registers the "Primary" navigation.

```php
namespace Tonik\Theme\App\Structure;

use function Tonik\Theme\App\config;

function register_navigation_areas()
{
  register_nav_menus([
    'primary' => __('Primary', config('textdomain')),
  ]);
}
add_action('after_setup_theme', 'Tonik\Theme\App\Structure\register_navigation_areas');
```

Add new entries to the array in order to register additional navigations. Assist yourself by using `config()` function to localize menu titles.

```php
namespace Tonik\Theme\App\Structure;

use function Tonik\Theme\App\config;

function register_navigation_areas()
{
  register_nav_menus([
    'primary' => __('Primary', config('textdomain')),
    'secondary' => __('Secondary', config('textdomain')),
  ]);
}
add_action('after_setup_theme', 'Tonik\Theme\App\Structure\register_navigation_areas');
```

## Usage

Use `wp_nav_menu` to output menu assigned to previously registered navigation area.

```php
wp_nav_menu([
  'theme_location' => 'secondary'
]);
```
