---
extends: docs
title: "Registering custom post types"
group: "Basics"
subgroup: "Structure"
prev: using-service-container
next: registering-custom-taxonomies
order: 1
---

Post types allow you to easily create and manage various content structures.

They should be registered inside `app/Structure/posttypes.php` file within `init` action. Starter registers `book` post type as an example. Customize it to your needs.

```php
namespace Tonik\Theme\App\Structure;

use function Tonik\Theme\App\config;

function register_book_post_type()
{
  register_post_type('book', [
    'description' => __('Collection of books.', config('textdomain')),
    'supports' => ['title', 'editor', 'excerpt', 'thumbnail'],
    'public' => true,
  ]);
}
add_action('init', 'Tonik\Theme\App\Structure\register_book_post_type');
```
