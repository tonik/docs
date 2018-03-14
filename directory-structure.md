---
extends: docs
title: "Directory structure"
group: "Basics"
subgroup: "General"
prev: deployment
next: creating-templates
order: 1
---

This starter theme introduces "easy to follow" folder structure, which enforces to divide your theme logic into separate files. For quick overview take a look at the structure tree bellow.

```
theme                              # — Root of your theme
   ├── app/                        # — Theme application logic
   │   ├── Http/                   # — Http layer of theme
   │   ├── Setup/                  # — Setups for theme
   │   ├── Structure/              # — Structures for theme
   ├── build/                      # — Webpack builder configuration and instruction files
   ├── bootstrap/                  # — Files responsible for bootstrapping a theme
   ├── config/                     # — Theme's Configuration files
   ├── public/                     # — Front-end compiled/builded assets (don't edit)
   ├── resources/                  # — Resources files
   │   ├── assets                  # — Front-end source assets
   │   │   ├── js                  # — Theme's JavaScript files
   │   │   ├── sass                # — Theme's Stylesheets files
   │   │   ├── images              # — Theme's images
   │   │   ├── fonts               # — Theme's fonts
   │   ├── languages               # — Theme's localization files
   │   ├── templates               # — Theme's template files
```

#### `app/`

General folder for components of your theme. All of the autoloaded files of your theme will be stored in this directory. Folder structure inside is not strict, feel free to adjust it to your preferences.

- `Http` - Modules responsible for registering theme's stylesheets and javascript files or defining AJAX responses
- `Setup` - Modules to adjust various parts of the WordPress like actions, filters or supports by theme
- `Structure` - Modules that registers structures like custom post types, navigations or sidebars

#### `bootstrap/`

This directory contains all files which are called when a theme is bootstrapped. They look for required dependencies and initializing theme itself. You probably do not need to change anything here.

#### `build/`

Includes all procedures of theme builder i.e. Webpack configuration and rules files which determines how theme's front-end is compiled.

#### `config/`

The `config` directory stores all of your theme's configuration files. You will find here configurations for both theme and builder.

#### `resources/`

The resources directory includes your templates as well as un-compiled assets like SASS, or JavaScript. You will also find here language files.

- `assets/sass/` - Un-compiled sass styles
- `assets/js/` - Un-compiled scripts
- `assets/fonts/` - font files
- `assets/images/` - static images
- `templates/` - `.tpl.php` template files
- `languages/` - `.po` and `.mo` translation files

#### `public/`

This directory contains all your compiled and optimized assets such as images, scripts, and stylesheets. It is important to remember that this directory is removed entirely before each build, so you should not make changes in files inside this folder.
