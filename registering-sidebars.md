---
extends: docs
title: "Registering sidebars"
group: "Basics"
subgroup: "Structure"
prev: adding-thumbnail-sizes
next: adding-shortcodes
order: 5
---

The sidebars are areas (managed in "Appearance > Widgets") where you can allocate customizable widgets and display it in the specified place.

You should register your sidebars inside `app/Setup/sidebars.php` file with `register_sidebar` function within `widgets_init` action hook. Inside `sidebars.php` you will see an example sidebar. Customize it to your needs or add another one.

```php
namespace Tonik\Theme\App\Structure;

use function Tonik\Theme\App\config;

function register_widget_areas()
{
  register_sidebar([
    'id' => 'sidebar',
    'name' => __('Sidebar', config('textdomain')),
    'description' => __('Website sidebar', config('textdomain')),
  ]);
}
add_action('widgets_init', 'Tonik\Theme\App\Structure\register_widget_areas');
```

## Usage

To render sidebar content just run `dynamic_sidebar` function with a previously registered sidebar name.

```php
dynamic_sidebar('sidebar');
```
