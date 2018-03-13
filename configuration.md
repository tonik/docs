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
- `{{ theme.parent }}` - Name of the parent theme, if initializing child theme.

## Initiating with CLI

Starter comes with simple CLI and `tonik` command, which allows you to easily fill these theme details and information. Simply call `vendor/bin/tonik` command in the theme root directory. A setup wizard will guide you through the entire process.

```bash
# Run setup wizard.
$ vendor/bin/tonik
```

> Take a note that a path to CLI file may be different if you specified custom `vendor` folder localization in `composer.json` file.

## Configuration Files

General configuration settings of a theme are stored in the `config/` directory and main `style.css` file.

#### `style.css`

Standard theme stylesheet file. Defines all details about the theme displayed in the admin panel. Refer to [Codex](https://codex.wordpress.org/Theme_Development#Theme_Stylesheet) for more information.

#### `config/app.php`

Configuration for theme structure paths, files to autoload and other settings of core functionalities. Each option has a short description to let you know about the usage.

> You can easily access these configuration values using the global `config` helper function. Read about this in [Helper functions](/theme/docs/helper-functions/) documentation.

#### `config/app.json`

This configuration file is used by theme builder during the build process. It defines a list of front-end assets used by a theme. It also setups builder and development settings.

> You will find a complete guide about handling theme assets in [Registering stylesheet and scripts](/theme/docs/registering-stylesheets-and-scripts/) and [Development](/theme/docs/development/) documentation.

## Environment configuration

It is useful to have different builder configuration based on the environment where the application is running. For example, developers may use various local development stacks and may need to set up different BrowserSync configurations.

Inside a theme's root folder you will find a sample `.env.example` file. Rename the file to `.env` and adjust variables inside as needed. Review the file `build/app.config.js` file to see all available environment variables.

> Your .env file should not be committed to your application's source control.

### Setting up BroswerSync

[BroswerSync](//browsersync.io/) can monitor your files for changes and automatically refresh browser for you. Configure its settings in `.env` file and start Webpack's development server using the `npm run watch` command. Now, after every file modification, your changes will be instantly reflected in the browser.

```
BROWSERSYNC_HOST="localhost"
BROWSERSYNC_PORT=3000
BROWSERSYNC_PROXY="http://localhost:8080/"
```

For example, if you are using [Wocker](//wckr.github.io/), simply pass `wocker.test` domain as a proxy field value. After you should be able to visit your WordPress installation at http://localhost:3000/ address.

```
BROWSERSYNC_HOST="localhost"
BROWSERSYNC_PORT=3000
BROWSERSYNC_PROXY="http://wocker.test/"
```

### Linting project Stylesheets

You can configure linting rules for project in `.stylelintrc` file. By default, starter setups only 4 space indentation. It doesn't enforce you to uncomfortable settings, so feel free to add here your own set of rules. You can find all available rules on [Stylelint website](//stylelint.io/user-guide/rules/).

```json
{
  "rules": {
    "indentation": 4
  }
}
```

### Linting project JavaScript

JavaScript linting rules can be configured in `.eslintrc` file. You can find all available rules on [ESLint website](//eslint.org/docs/rules/).

```json
{
  "rules": {
    "indent": ["error", 2]
  }
}
```