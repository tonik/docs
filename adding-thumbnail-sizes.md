---
extends: docs
title: "Adding thumbnail sizes"
group: "Basics"
subgroup: "Structure"
---

Registering own thumbnails allows for creating additional images sizes, beyond those shipped with WordPress. Your new image sizes should be registered inside `app/Setup/thumbnails.php` file with `add_image_size` function within `after_setup_theme` action hook.

```php
namespace App\Theme\Structure;

function add_image_sizes()
{
  add_image_size('custom-thumbnail', 800, 600, true);
}
add_action('after_setup_theme', 'App\Theme\Structure\add_image_sizes');
```

## Usage

Reference name of newly created image size when outputting images.

```php
the_post_thumbnail('custom-thumbnail');
```
