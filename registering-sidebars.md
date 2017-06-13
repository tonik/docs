---
extends: docs
title: "Registering sidebars"
group: "Basics"
subgroup: "Structure"
---

The sidebars are areas (managed in `Appearance > Widgets`) where you can allocate customizable widgets and display it in the specified place. You should register your sidebars inside `app/Setup/sidebars.php` file with `register_sidebar` function within `widgets_init` action hook.

Inside `sidebars.php` you will see an example sidebar. Customize it to your needs or add another one.

<pre class="pre"><code class="language-php">namespace App\Theme\Structure;

use function App\Theme\config;

function register_widget_areas()
{
    register_sidebar([
        'id' => 'sidebar',
        'name' => __('Sidebar', config('textdomain')),
        'description' => __('Website sidebar', config('textdomain')),
    ]);
}
add_action('widgets_init', 'App\Theme\Structure\register_widget_areas');</code></pre>

## Usage

To render sidebar content just run `dynamic_sidebar` function with a previously registered sidebar name.

<pre class="pre"><code class="language-php">dynamic_sidebar('sidebar');</code></pre>
