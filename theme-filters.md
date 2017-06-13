---
extends: docs
title: "Theme filters"
group: "Basics"
section: "Setup"
---

Filters can change an output or behavior of different parts of your theme or WordPress. They should be defined inside `app/Setup/filters.php` file.

Inside you can see a standard example of modifying the length of the excerpt.

<pre class="pre"><code class="language-php">namespace App\Theme\Setup;

function modify_excerpt_length()
{
    return 60;
}
add_filter('excerpt_length', 'App\Theme\Setup\modify_excerpt_length');</code></pre>

## Examples

### Using filters to control sidebar visibility

Controlling sidebar visibility is a great use case for custom filters. Let's start with creating markup of our sidebar inside filtered conditional.

<pre class="pre"><code class="language-html"><?php if (apply_filters('theme/sidebar/visibility', true)): ?>
    <aside>
        <?php get_sidebar() ?>
    </aside>
<?php endif ?></code></pre>

Create a filter which hides the sidebar on a page with 404 error view.

<pre class="pre"><code class="language-php">namespace App\Theme\Setup;

function display_sidebar($status)
{
    $conditions = [is_404(), is_page()];

    if (in_array(true, $conditions)) {
        return false;
    }

    return $status;
}
add_filter('theme/sidebar/visibility', 'App\Theme\Setup\display_sidebar');</code></pre>
