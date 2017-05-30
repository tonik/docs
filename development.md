---
title: "Development"
group: "Getting Started"
---

## Required tools

Theme uses [NPM](//www.npmjs.com/) as a front-end dependency manager and [Composer](//getcomposer.org/) as a back-end dependency manager. Make sure your development machine has installed following dependencies:

- [Node.js](//nodejs.org/)
- [NPM](//www.npmjs.com/)
- [Composer](//getcomposer.org/)

## Building a Theme

[Webpack](https://webpack.js.org/) is used to compile and optimize theme's scripts, stylesheets, and images.

#### Resolving dependencies

Before be able to build theme you have to resolve required dependencies.

```bash
# @ wp-content/themes/<theme-name>

# Install composer dependencies.
$ composer install

# Install node dependencies.
$ npm install
```

Now you have all the packages necessary to run the build process and start developing your theme.

#### Building a Theme

There are a few available commands which help you to build the theme for different environments:

```bash
# @ wp-content/themes/<theme-name>

# Compiles unminified and unoptimized theme assets with source maps.
$ npm run development

# Alias for `development` command.
$ npm run dev

# Compiles minified and optimized theme assets without source maps.
$ npm run production

# Alias for `production` command.
$ npm run prod

# Builds assets for development, runs watcher (recompiles on change)
# and BroswerSync (refreshes browser).
$ npm run watch
```

## Handling project dependencies

### Front-end dependencies

All of the front-end packages necessary for your theme can be found in the `package.json`. Of course, you can specify and install other packages required by your project with [`npm install`](https://docs.npmjs.com/cli/install) command or by adding additional fields to the `package.json` file.

```bash
# @ wp-content/themes/<theme-name>
npm install foundation-sites
```

Builder helps you also with importing third-party stylesheet libraries. Instead of referring path directly to the `node_modules/` directory, simply include it with `~` at the beginning. Builder will take care of it for you.

```scss
@import '~foundation-sites/scss/foundation';
```

Thanks to Babel you can use all of [ES6](https://babeljs.io/learn-es2015/) goodness. Especially, importing external scripts as modules.

```js
// CommonJS
require('foundation-sites')

// ES6 Modules
import $ from 'jquery'
```

### Backend-end dependencies

The starter is configured to pull in Composer’s autoload file. All you need to do is require the desired package.

```bash
# @ wp-content/themes/<theme-name>
composer require monolog/monolog
```

Afterward, it will be available inside every component of the project. Just import package namespaces and use it.

```php
use Monolog\Logger;
use Monolog\Handler\StreamHandler;
```

## Environment configuration

### Setting up BroswerSync

[BroswerSync](//browsersync.io/) can monitor your files for changes and automatically refresh browser for you.

Configure its settings in `config/app.json` file and start Webpack's development server using the `npm run watch` command. Now, after every file modification, your changes will be instantly reflected in the browser.

```json
"settings": {
  "browserSync": {
    "host": "localhost",
    "port": 3000,
    "proxy": "http://localhost:8080/"
  }
}
```

For example, if you are using [Wocker](//wckr.github.io/), simply pass `wocker.dev` domain as a proxy field value. After you should be able to visit your WordPress installation at http://localhost:3000/ address.

```json
"settings": {
  "browserSync": {
    "host": "localhost",
    "port": 3000,
    "proxy": "http://wocker.dev/"
  }
}
```

### Linting project stylesheets

You can configure linting rules for project in `.stylelintrc` file. By default, starter setups only 4 space indentation. It doesn't enforce you to uncomfortable settings, so feel free to add here your own set of rules. You can find all available rules on [Stylelint website](https://stylelint.io/user-guide/rules/).

```json
{
  "rules": {
    "indentation": 4
  }
}
```

## Customizing build process

Builder rules and procedures are stored in the `build/` directory. Default settings of builder are contained in a `webpack.config.js` and `app.config.js` files. These settings are extended with theme's `config/app.json` configuration file where you can easily overwrite defaults.

### Customizing assets filenames and output paths

You can control outputted names with `outputs` property in `config/app.json` file. Object structure should look like this:

```json
"outputs": {
  "css": { "filename": "css/[name].css" },
  "font": { "filename": "fonts/[name].[ext]" },
  "image": { "filename": "images/[name].[ext]" },
  "javascript": { "filename": "js/[name].js" }
}
```

As you see, filenames have to use [Webpack placeholders](https://webpack.js.org/configuration/output/#output-filename) to determine asset name or extension.

### Giving access to the global variables inside theme's scripts

To bypass conflicts with global variables, scripts outputted by Webpack are enclosed inside scope. This force you to say explicitly which external variables you want inside theme scripts.

By default, starter gives you access to the jQuery shipped with WordPress.

```json
"externals": {
  "jquery": "jQuery"
}
```

Simply add to the list new entry where the key is a name (under which external will be available) and the name of the global variable as value.

```json
"externals": {
  "jquery": "jQuery",
  "backbone": "Backbone"
}
```

Now, you can import this variable inside your theme scripts.

```js
import Backbone from 'backbone'
```

### Additional features settings

Additional features can be configured within `settings` property.

```json
"settings": {
  "browserSync": {
    "host": "localhost",
    "port": 3000,
    "proxy": "http://localhost:8080/"
  }
}
```

List of available options:

- `browserSync` - {Object} - Settings for [BroswerSync](//github.com/Va1/browser-sync-webpack-plugin) plugin.
- `sourceMaps` - {Boolean} - Output assets source maps. Default to `true`.
- `styleLint` - {Boolean} - Lint project stylesheets. Default to `true`.