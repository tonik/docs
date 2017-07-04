---
extends: docs
title: "Installation"
group: "Getting Started"
prev: introduction
next: configuration
order: 2
---

Tonik Starter Theme uses [Composer](https://getcomposer.org/) and [NPM](https://www.npmjs.com/) to manage its dependencies. Make sure you have both installed on your machine before using this starter.

## Dependencies

A starter has a few dependencies. They are extracted to separate packages for easy installation and managing via Composer and NPM package managers.

- [tonik/gin](https://github.com/tonik/gin) (required) - Theme foundation which provides all custom functionalities
- [tonik/cli](https://github.com/tonik/cli) (optional) - Simple CLI for initiating theme

## Creating New Theme

WordPress themes lives in the `wp-content/themes` folder. This is where we have to fetch our fresh starter files.

```bash
# Go to the `themes` directory of your WordPress installation.
$ cd wp-content/themes
```

Create project via `composer create-project` composer command.

```bash
$ composer create-project tonik/theme <theme-name>
```

You can also directly download or clone the repository to the `wp-content/themes` directory.

```bash
# Clone repository to the <theme-name> folder.
$ git clone -b master git@github.com:tonik/theme.git <theme-name>
```

## Resolving Theme Dependencies

> You will find more detailed instructions about managing and building a theme in [Development](/theme/docs/development/) documentation.

In order to property bootstrap a theme you have to fetch some required dependencies and compile its assets. Before that, make sure that you are in the root folder of the theme (where `package.json` and `composer.json` files are located).

```bash
# @ wp-content/themes
$ cd <theme-name>
```

#### 1. Install back-end dependencies and generate an autoloading file.

```bash
# Install composer dependencies.
$ composer install
```

#### 2. Install front-end dependencies and builder.

```bash
# Install node dependencies.
$ npm install
```

#### 3. Build a Theme

Let's prebuild the theme to avoid error about missing enqueued assets.

```bash
# Build a theme for development.
$ npm run dev
```

## Activate Theme

Now, you are ready to turn on your newly created theme. Go to the WordPress admin panel and activate the theme on `Appearance > Themes` page. Familiar with WP-CLI? Use `theme activate` command.

```bash
# Activate newly created theme.
$ wp theme activate <theme-name>
```
