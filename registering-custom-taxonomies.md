---
extends: docs
title: "Registering custom taxonomies"
group: "Basics"
subgroup: "Structure"
---

Taxonomy allows for classifying your posts in groups. They should be registered inside `app/Structure/taxonomies.php` file within `init` action.

Starter registers `book_genre` taxonomy as an example. Customize it to your needs.

<pre class="pre"><code class="language-php">namespace App\Theme\Structure;

function register_book_genre_taxonomy()
{
    register_taxonomy('book_genre', 'book', [
        'rewrite' => [
            'slug' => 'books/genre',
            'with_front' => true,
            'hierarchical' => true,
        ],
        'hierarchical' => true,
        'public' => true,
    ]);
}
add_action('init', 'App\Theme\Structure\register_book_genre_taxonomy');</code></pre>
