---
extends: docs
title: "Theme actions"
group: "Basics"
subgroup: "Setup"
---

Actions allow you to trigger various logic at the specific moments and places when executing your application. They should be registered inside `app/Setup/actions.php` file.

As a simple example, let's output `Hello World` to the footer.

<pre class="pre"><code class="language-php">namespace App\Theme\Setup;

function render_text()
{
    echo "Hello world!";
}
add_action('wp_footer', 'App\Theme\Setup\render_text');</code></pre>

## Examples

### Rendering template partials with actions

Start with making a `single.tpl.php` post template with side content, but instead of immediately outputting the sidebar body, execute custom `theme/single/sidebar` action. You will later hook to that action in order to render actual sidebar.

<pre class="pre"><code class="language-html"><!-- @ resources/templates/single.tpl.php -->

<aside>
    <?php do_action('theme/single/sidebar') ?>
</aside></code></pre>

Next, create the `sidebar.tpl.php` where you will output specified sidebar with `dynamic_sidebar` function.

<pre class="pre"><code class="language-html"><!-- @ resources/templates/partials/sidebar.tpl.php -->

<?php if (is_active_sidebar('sidebar')) : ?>
    <?php dynamic_sidebar('sidebar') ?>
<?php else: ?>
    <h5>Sidebar</h5>
    <p>Your sidebar is empty.</p>
<?php endif; ?></code></pre>

We also need main controller file for sidebar itself. It should just render `sidebar.tpl.php` template.

<pre class="pre"><code class="language-php">// @ sidebar.php

namespace App\Theme;

use function App\Theme\template;

template('partials/sidebar');</code></pre>

Finally, hook to previously created action inside `single.tpl.php` and output sidebar (the `sidebar.php` file) with `get_sidebar()` function.

<pre class="pre"><code class="language-php">// @ app/Setup/actions.php

namespace App\Theme\Setup;

function render_sidebar()
{
    get_sidebar();
}
add_action('theme/single/sidebar', 'App\Theme\Setup\render_sidebar');</code></pre>
