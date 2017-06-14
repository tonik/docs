---
extends: docs
title: "Defining AJAX responses"
group: "Basics"
subgroup: "Http"
---

WordPress gives you an ability to define various AJAX actions, which you can afterward hit with HTTP requests in order to create dynamic JavaScript components for your theme.

Your ajax listeners should be registered inside `app/Http/ajaxes.php` file.

> Please refer to the [Codex](https://codex.wordpress.org/AJAX_in_Plugins) documentation for comprehensive guides about creating AJAX actions.

### 1. Provide Ajax URL for script

Your scripts need to know an URL endpoint, where they can reach your registered actions. Start with providing an Admin AJAX URL, by localizing your script with data. Use `admin_url()` function to pull URL for AJAX calls.

```php
wp_register_script('script-ajax', asset_path('js/script-ajax.js'), ['jquery'], null, true);

wp_localize_script('script-ajax', 'Ajax', [
  'ajax' => [
    'url' => admin_url('admin-ajax.php')
  ],
]);

wp_enqueue_script('script-ajax');
```

### 2. Listen for action

Register listener for your AJAX action.

```php
namespace App\Theme\Http;

function handle_ajax_action()
{
  // Action logic...

  die();
}
add_action('wp_ajax_my_action', 'App\Theme\Http\handle_ajax_action');
add_action('wp_ajax_nopriv_my_action', 'App\Theme\Http\handle_ajax_action');
```

### 3. Calling actions from JavaScript

As an example, we will use $.ajax() to perform an asynchronous HTTP request to our action endpoint.

```js
$.ajax({
  url: Ajax.url,
  dataType: 'json',
  data: {
    action: 'my_action' // Your AJAX action name
  }
}).done(function(data, status, response) {
  // Callback
});
```
