---
extends: docs
title: "Registering stylesheets and scripts"
group: "Basics"
subgroup: "Http"
prev: helper-functions
next: defining-ajax-responses
order: 1
---

## Workflow

Inside your theme's `config/app.json` you will find `assets` property. It holds a list of file paths which will be processed by the builder and outputted to the `public` directory.

As you can see, by default, we already building main stylesheets and scripts of theme and framework.

```json
"assets": {
  "app": [
    "./resources/assets/js/app.js",
    "./resources/assets/sass/app.scss"
  ],

  "foundation": [
    "./resources/assets/js/foundation.js",
    "./resources/assets/sass/foundation.scss"
  ]
}
```

Let's assume you need to add additional script. It will be loaded separately, only on the specific page.

### 1. Create new assets files.

Of course, you have to start with creating an actual file in a proper `resources/assets` folder.

### 2. Add assets to the builder list

Provide an array of assets file paths to the `assets` list. They should be registered under a unique property key name.

```json
"assets": {
  "app": [
    "./resources/assets/js/app.js",
    "./resources/assets/sass/app.scss"
  ],

  "foundation": [
    "./resources/assets/js/foundation.js",
    "./resources/assets/sass/foundation.scss"
  ],

  "shop-finder": [
    "./resources/assets/js/shop-finder.js",
    "./resources/assets/sass/shop-finder.scss"
  ]
}
```

### 3. Register and enqueue assets in WordPress

Your assets should be enqueued inside `app/Http/assets.php` file in `register_stylesheets` or `register_scripts` functions which are hooked to the `wp_enqueue_scripts` action.

> For referencing paths for assets you should use the `asset_path()` function. You can learn more about this function in [Helper functions](/theme/docs/helper-functions/) documentation.

```php
/**
 * Registers theme stylesheet files.
 *
 * @return void
 */
function register_stylesheets() {
  wp_enqueue_style('foundation', asset_path('css/foundation.css'));
  wp_enqueue_style('app', asset_path('css/app.css'));

  if (is_page('shops')) {
    wp_enqueue_style('shop-finder', asset_path('css/shop-finder.css'));
  }
}
add_action('wp_enqueue_scripts', 'Tonik\Theme\App\Http\register_stylesheets');
```

```php
/**
 * Registers theme script files.
 *
 * @return void
 */
function register_scripts() {
  wp_enqueue_script('foundation', asset_path('js/foundation.js'), ['jquery'], null, true);
  wp_enqueue_script('app', asset_path('js/app.js'), ['foundation'], null, true);

  if (is_page('shops')) {
    wp_enqueue_script('shop-finder', asset_path('js/shop-finder.js'), ['jquery'], null, true);
  }
}
add_action('wp_enqueue_scripts', 'Tonik\Theme\App\Http\register_scripts');
```

### 4. Run theme builder

Finally, you have to run builder to compile newly added assets.

```bash
# @ wp-content/themes/<theme-name>
npm run dev
```
