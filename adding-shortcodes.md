---
extends: docs
title: "Adding shortcodes"
group: "Basics"
section: "Structure"
---

Shortcodes allow you to easily embed a dynamic content into the body of a page or post as a simple string. You should register your custom shortcodes in `app/Structure/shortcodes.php` with `add_shortcode` function.

Start with determining the structure of your custom shortcode.

```
[shortcode attr="attribute"]Content[/shortcode]
```

Next, register shortcode handler function.

```php
namespace App\Theme\Structure;

function render_shortcode($atts, $content)
{
    // $atts: ['attr' => 'attribute']
    // $content: 'Content'
}
add_shortcode('shortcode', 'App\Theme\Structure\render_shortcode');
```

## Examples

### Rendering button with `template()` helper function

You may use `template()` function to render markup of elements. It is a great way to maintain separation of presentation logic and business logic.

Your handler function needs to return a string instead of outputting. We can achieve this by starting output buffer before using `template` function and returning content of the buffer from the handler.

```php
namespace App\Theme\Structure;

function render_button_shortcode($atts, $content)
{
    $attributes = shortcode_atts([
        'href' => '#'
    ], $atts);

    ob_start();

    template('shortcodes/button', compact('attributes', 'content'));

    return ob_get_clean();
}
add_shortcode('button', 'App\Theme\Structure\render_button_shortcode');
```