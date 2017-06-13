---
extends: docs
title: "Installation"
group: "Getting Started"
---

Tonik Starter Theme uses [Composer](https://getcomposer.org/) and [NPM](https://www.npmjs.com/) to manage its dependencies. Make sure you have both installed on your machine before using this starter.

## Dependencies

A starter has a few dependencies. They are extracted to separate packages for easy installation and managing via Composer and NPM package managers.

- [tonik/gin](https://github.com/tonik/gin) (required) - Theme foundation which provides all custom functionalities
- [tonik/cli](https://github.com/tonik/cli) (optional) - Simple CLI for initiating theme

## Creating New Theme

WordPress themes lives in the `wp-content/themes` folder. This is where we have to fetch our fresh starter files.

<pre class="pre pre--dark"><code class="language-bash"># Go to the `themes` directory of your WordPress installation.
$ cd wp-content/themes</code></pre>

Create project via `composer create-project` composer command.

<pre class="pre pre--dark"><code class="language-bash">$ composer create-project tonik/tonik <theme-name></code></pre>

You can also directly download or clone the repository to the `wp-content/themes` directory.

<pre class="pre pre--dark"><code class="language-bash"># Clone repository to the <theme-name> folder.
$ git clone git@github.com:tonik/tonik.git <theme-name></code></pre>

## Resolving Theme Dependencies

> You will find more detailed instructions about managing and building a theme in [Development](https://github.com/tonik/tonik/wiki/Development) documentation.

In order to property bootstrap a theme you have to fetch some required dependencies and compile its assets. Before that, make sure that you are in the root folder of the theme (where `package.json` and `composer.json` files are located).

<pre class="pre pre--dark"><code class="language-bash"># @ wp-content/themes
$ cd <theme-name></code></pre>

#### 1. Install back-end dependencies and generate an autoloading file.

<pre class="pre pre--dark"><code class="language-bash"># Install composer dependencies.
$ composer install</code></pre>

#### 2. Install front-end dependencies and builder.

<pre class="pre pre--dark"><code class="language-bash"># Install node dependencies.
$ npm install</code></pre>

#### 3. Build a Theme

Let's prebuild the theme to avoid error about missing enqueued assets.

<pre class="pre pre--dark"><code class="language-bash"># Build a theme for development.
$ npm run dev</code></pre>

## Activate Theme

Now, you are ready to turn on your newly created theme. Go to the WordPress admin panel and activate the theme on `Appearance > Themes` page. Familiar with WP-CLI? Use `theme activate` command.

<pre class="pre pre--dark"><code class="language-bash"># Activate newly created theme.
$ wp theme activate <theme-name></code></pre>
