---
extends: docs
title: "Child Theme Development"
group: "Extending"
prev: integrating-advanced-custom-fields
next: asset
order: 2
---

The Tonik Starter Theme supports a standard parent-child theme workflow. However, if you would like to use same structure and functionalities as parent theme we encourage you to take a look at our [child theme boilerplate](https://github.com/tonik/child-theme).

## Installation

WordPress child theme should be placed in the same `wp-content/themes` folder as parent theme. Here we have to fetch our fresh starter files.

### 1. Creating New Child Theme

```bash
# Go to the `themes` directory of your WordPress installation.
$ cd wp-content/themes
```

Create project via `composer create-project` composer command.

```bash
$ composer create-project tonik/child-theme <theme-name>
```

You can also directly download or clone the repository to the `wp-content/themes` directory.

```bash
# Clone repository to the <theme-name> folder.
$ git clone -b master git@github.com:tonik/child-theme.git <theme-name>
```

### 2. Resolving Child Theme Dependencies

Child theme only downloads only one optional dependency, a CLI.

```bash
# Install composer dependencies.
$ composer install
```

### 3. Activate Child Theme

Now, you are ready to turn on your newly created theme. Go to the WordPress admin panel and activate the theme on `Appearance > Themes` page. Familiar with WP-CLI? Use `theme activate` command.

```bash
# Activate newly created child theme.
$ wp theme activate <theme-name>
```

## Configuration

Starter uses special placeholder strings for various theme details and information (like name, description and project textdomain). Child Theme additionaly introduces a `{{ theme.parent }}` placeholder for defining a folder name of the parent theme.

## Initiating with CLI

Child themes can be also initialized with our CLI and fill placeholders for you. A setup wizard will guide you through the entire process.

```bash
# Run setup wizard.
$ vendor/bin/tonik
```

## Directory Structure

Structure of a child theme is quite simlar to the parent.

```
child-theme              # — Root of your theme
   ├── app/              # — Parent Theme application logic (overwrites parent)
   ├── child/            # — Child Theme application logic
   │   ├── Http/         # — Http layer of child theme
   │   ├── Setup/        # — Setups for child theme
   ├── build/            # — Webpack builder configuration and instruction files
   ├── bootstrap/        # — Files responsible for bootstrapping a theme
   ├── config/           # — Child Theme's Configuration files
   ├── public/           # — Front-end compiled/builded assets (don't edit)
   ├── resources/        # — Resources files
   │   ├── languages     # — Child Theme's localization files
   │   ├── templates     # — Child Theme's template files (overwrites parent)
```

#### `child/`

Holds child theme specific components. Files it this folder are additionaly by child theme in `functions.php` file.

- `Http` - Modules responsible for registering child theme's stylesheets and javascript files
- `Setup` - Modules to adjust various parts of the WordPress like actions, filters or supports by child theme

## Developing

By default child boilerplate do not comes with builder or task runner for theme's assets. However, if you need it, you can copy relevant Webpack configuration files and settings directly from a parent theme.

### Overwriting Parent Files

Autoload and Template components uses `localize_template` to include files, so parent files can be easily overwrited by child theme. They only have to be accessible at the same path as they are in the parent. 

For example, let's overwrite one of the parent template file. Assume that parent contains a `footer.tpl.php` file in `resources/templates` directory. Now to  you just have to create same file at the same filepath in child theme.

### Understanding a Service Container

It's important to understood that a service container is shared across parent and child theme. Thanks to this you have access to all services defined in parent theme and you can easily use it directly in child theme files.

However, this enforces you to namespace new services defined at child level. It is recommended to prefix service names with `child` keyword.

```php
theme()->bind('child.service', function() {
  // Child specific service
});
```

### Accessing Child and Parent Theme Configs

After learning about prefixes from previous paragraphIt is now clear that child theme configuration can be accessed at `child.config` service name.

```php
// Gets child theme config values.
$config = theme('child.config');
```

A call to `config` service will still return a parent theme configuration values.

```php
// Gets parent theme config values.
$config = theme('config');
```