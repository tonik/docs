---
extends: docs
title: "Configuration"
group: "Getting Started"
prev: installation
next: development
order: 3
---

## Placeholders

Starter uses special placeholder strings for various theme details and information (like name, description and project textdomain), so you can simply find and replace it with your editor.

> Our CLI can fill these fields for you. More details in the next section.

Here a list of all used placeholders with descriptions:

- `{{ theme.name }}` - Theme name.
- `{{ theme.url }}` - URL to the theme.
- `{{ theme.description }}` - Theme short description.
- `{{ theme.version }}` - Theme version number.
- `{{ theme.author }}` - Theme author name.
- `{{ theme.author.url }}` - Website of theme author.
- `{{ theme.textdomain }}` - Theme textdomain string for gettext localization.

## Initiating with CLI

Starter comes with simple CLI and `tonik` command, which allows you to easily fill these theme details and information. Simply call `vendor/bin/tonik` command in the theme root directory. A setup wizard will guide you through the entire process.

> Take a note that a path to CLI file may be different if you specified custom `vendor` folder localization in `composer.json` file.

```bash
# Run setup wizard.
$ vendor/bin/tonik
```

## Configuration Files

All of the configuration settings of a theme are stored in the `config/` directory and main `style.css` file.

#### `style.css`

Standard theme stylesheet file. Defines all details about the theme displayed in admin panel. Refer to [Codex](https://codex.wordpress.org/Theme_Development#Theme_Stylesheet) for more information.

#### `config/app.php`

Configuration for theme structure paths, files to autoload and other settings of core functionalities. Each option has a short description to let you know about the usage.

> You can easily access these configuration values using the global `config` helper function. Read about this in [Helper functions](/theme/docs/helper-functions/) documentation.

#### `config/app.json`

This configuration file is used by theme builder during the build process. It defines a list of a front-end assets used by a theme. It also setups builder and development settings.

> You will find a complete guide about handling theme assets in [Registering stylesheet and scripts](/theme/docs/registering-stylesheets-and-scripts/) and [Development](/theme/docs/development/) documentation.
