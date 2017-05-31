---
extends: _layouts.docs
title: "Dirctory structure"
group: "Basics"
---

This starter theme introduces "easy to follow" folder structure, which enforces to divide your theme logic into separate files. For quick overview take a look at the structure tree bellow.

```
theme                               # — Root of your theme
    ├── app/                        # — Theme application logic
    │   ├── Http/                   # — Http layer of theme
    │   │   ├── ajaxes.php          # — Theme ajaxes endpoints
    │   │   ├── assets.php          # — Theme styles and scripts loading
    │   ├── Setup/                  # — Setups for theme
    │   │   ├── actions.php         # — Theme action hooks
    │   │   ├── filters.php         # — Theme filter hooks
    │   │   ├── navs.php            # — Theme navigation areas
    │   │   ├── shortcodes.php      # — Theme shortcodes
    │   │   ├── sidebars.php        # — Theme widgets areas
    │   │   ├── supports.php        # — Theme supports
    │   │   ├── thumbnails.php      # — Theme custom image sizes
    │   │   ├── widgets.php         # — Theme custom widgets
    │   ├── Structure/              # — Structures for theme
    │   │   ├── posttypes.php       # — Theme custom post types
    │   │   ├── taxonomies.php      # — Theme custom taxonomies
    │   ├── helpers.php             # — Collection of helper functions
    ├── build/                      # — Webpack configuration and instruction files
    ├── bootstrap/                  # — Files responsible for bootstrapping a theme
    │   ├── compatibility.php       # — Theme compatibility checker (don't edit)
    │   ├── theme.php               # — Theme bootstraper script (don't edit)
    ├── config/                     # — Configuration files
    │   ├── app.json                # — Theme assets manifest file
    │   ├── app.php                 # — Theme configuration file
    ├── public/                     # — Front-end compiled/builded assets (don't edit)
    ├── resources/                  # — Resources files
    │   ├── assets                  # — Front-end source assets
    │   │   ├── js                  # — Theme JavaScript files
    │   │   ├── sass                # — Theme Stylesheets files
    │   │   ├── images              # — Theme images
    │   │   ├── fonts               # — Theme fonts
    │   ├── languages               # — Theme translations
    │   ├── templates               # — Theme templates
    ├── 404.php                     # — 404 page controller
    ├── composer.json               # — PHP dependences and PSR-4 Autoloading
    ├── footer.php                  # — Footer partial template
    ├── functions.php               # — Bootstrapping the theme. Initiates Autoloader and Composer (don't edit)
    ├── header.php                  # — Header partial template
    ├── index.php                   # — Index page controller
    ├── package.json                # — NPM dependencies and scripts
    ├── screenshot.png              # — Theme screenshot image
    ├── style.css                   # — Theme details information (don't write any CSS declarations in here)
```

### `app/`

General folder for components of your theme. All of the autoloaded files of your theme will be stored in this directory. Folder structure inside is not strict, feel free to adjust it to your preferences.

### `bootstrap/`

This directory contains all files which are called when a theme is bootstrapped. They look for required dependencies and initializing theme itself. You probably do not need to change anything here.

### `build/`

Includes all procedures of theme builder i.e. Webpack configuration and rules files which determines how theme's front-end is compiled.

### `config/`

The `config` directory stores all of your theme's configuration files. You will find here configurations for both theme and builder.

### `resources/`

The resources directory includes your templates as well as un-compiled assets like SASS, or JavaScript. You will also find here language files.

- `assets/sass/` - Un-compiled sass styles
- `assets/js/` - Un-compiled scripts
- `assets/fonts/` - font files
- `assets/images/` - static images
- `templates/` - `.tpl.php` template files
- `languages/` - `.po` and `.mo` translation files

### `public/`

This directory contains all your compiled and optimized assets such as images, scripts, and stylesheets. It is important to remember that this directory is removed entirely before each build, so you should not make changes in files inside this folder.