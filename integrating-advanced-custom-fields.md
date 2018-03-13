---
extends: docs
title: "Integrating Advanced Custom Fields"
group: "Extending"
prev: adding-shortcodes
next: child-theme-development
order: 1
---

[Advanced Custom Fields](https://www.advancedcustomfields.com) plugin allows you to create user-friendly administration pages and custom fields.

## Configuration

Advanced Custom Fields initiation files may be easily blended into a current folder structure. It's recommended to create additional `ACF/` directory inside `Structure/` folder. You can hold there all components related to ACF (like creating fields schema and custom admin pages).

```
theme
  ├── app/
  │   ├── Structure/
  │   │   ├── ACF/                # — Directory for ACF components
  │   │   │   ├── settings.php    # — Theme settings page configuration file
```

Remember to add a file path of the new component to autoload list inside a configuration file.

```php
'autoload' => [
  //...
  'Structure/ACF/settings.php',
  //...
]
```

## Examples

### Administration page for theme's general settings

Let's create the settings page for our theme.

```php
namespace Tonik\Theme\App\Structure\ACF;

use function Tonik\Theme\App\config;

acf_add_options_page([
  'page_title' => __('Theme Settings', config('textdomain')),
  'menu_title' => __('Theme Settings', config('textdomain')),
  'menu_slug' => 'theme-settings',
  'capability' => 'edit_posts',
  'redirect' => false
]);
```
