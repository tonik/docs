---
extends: docs
title: "Registering custom post types"
group: "Basics"
subgroup: "Structure"
---

Post types allow you to easily create and manage various content structures. They should be registered inside `app/Structure/posttypes.php` file within `init` action.

Starter registers `book` post type as an example. Customize it to your needs.

<pre class="pre"><code class="language-php">namespace App\Theme\Structure;

use function App\Theme\config;

function register_book_post_type()
{
    register_post_type('book', [
        'description' => __('Collection of books.', config('textdomain')),
        'supports' => ['title', 'editor', 'excerpt', 'thumbnail'],
        'public' => true,
    ]);
}
add_action('init', 'App\Theme\Structure\register_book_post_type');</code></pre>
