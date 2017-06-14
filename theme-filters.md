---
extends: docs
title: "Theme filters"
group: "Basics"
subgroup: "Setup"
---

Filters can change an output or behavior of different parts of your theme or WordPress. They should be defined inside `app/Setup/filters.php` file.

Inside you can see a standard example of modifying the length of the excerpt.

```php
namespace App\Theme\Setup;

function modify_excerpt_length()
{
  return 60;
}
add_filter('excerpt_length', 'App\Theme\Setup\modify_excerpt_length');
```

## Examples

### Using filters to control sidebar visibility

Controlling sidebar visibility is a great use case for custom filters. Let's start with creating markup of our sidebar inside filtered conditional.

```html
<?php if (apply_filters('theme/sidebar/visibility', true)): ?>
  <aside>
    <?php get_sidebar() ?>
  </aside>
<?php endif ?>
```

Create a filter which hides the sidebar on a page with 404 error view.

```php
namespace App\Theme\Setup;

function display_sidebar($status)
{
  $conditions = [is_404(), is_page()];

  if (in_array(true, $conditions)) {
    return false;
  }

  return $status;
}
add_filter('theme/sidebar/visibility', 'App\Theme\Setup\display_sidebar');
```
