---
extends: docs
title: "Adding menus and navigations"
group: "Basics"
section: "Structure"
---

Navigations allow for creating easily customizable menus areas, which can be managed inside `Appearance > Menus` administration panel. You should register navigations in `app/Structure/navs.php` file with `register_nav_menus` function.

By default, starter registers the "Primary" navigation.

<pre class="pre"><code class="language-php">namespace App\Theme\Structure;

use function App\Theme\config;

function register_navigation_areas()
{
    register_nav_menus([
        'primary' => __('Primary', config('textdomain')),
    ]);
}
add_action('after_setup_theme', 'App\Theme\Structure\register_navigation_areas');</code></pre>

Add new entries to the array in order to register additional navigations. Assist yourself by using `config()` function to localize menu titles.

<pre class="pre"><code class="language-php">namespace App\Theme\Structure;

use function App\Theme\config;

function register_navigation_areas()
{
    register_nav_menus([
        'primary' => __('Primary', config('textdomain')),
        'secondary' => __('Secondary', config('textdomain')),
    ]);
}
add_action('after_setup_theme', 'App\Theme\Structure\register_navigation_areas');</code></pre>

## Usage

Use `wp_nav_menu` to output menu assigned to previously registered navigation area.

<pre class="pre"><code class="language-php">wp_nav_menu([
    'theme_location' => 'secondary'
]);</code></pre>
