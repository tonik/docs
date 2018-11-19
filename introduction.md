---
extends: docs
title: "Introduction"
group: "Getting Started"
next: installation
order: 1
---

Tonik is a WordPress Starter Theme which aims to modernize, organize and enhance some aspects of WordPress theme development.

### Take a look at what is waiting for you:
- [ES6](https://babeljs.io/learn-es2015/) for JavaScript
- [SASS](http://sass-lang.com/) preprocessor for CSS
- [Webpack](https://webpack.js.org/) for managing, compiling and optimizing theme's asset files
- Simple [CLI](https://github.com/tonik/cli) for quickly initializing a new project
- Ready to use front-end boilerplates for [Foundation](//foundation.zurb.com/sites.html), [Bootstrap](//getbootstrap.com/docs/3.3/), [Bulma](//bulma.io/) and [Vue](//vuejs.org/)
- Utilizes PHP [Namespaces](http://php.net/manual/pl/language.namespaces.php)
- Simple [Theme Service Container](http://symfony.com/doc/2.0/glossary.html#term-service-container)
- Child Theme friendly [Autoloader](https://en.wikipedia.org/wiki/Autoload)
- Readable and centralized Theme Configs
- Oriented for building with [Actions](https://codex.wordpress.org/Glossary#Action) and [Filters](https://codex.wordpress.org/Glossary#Filter)
- Enhanced [Templating](https://en.wikibooks.org/wiki/PHP_Programming/Why_Templating) with support for passing data

### Requirements

Tonik Starter Theme follows [WordPress recommended requirements](https://wordpress.org/about/requirements/). Make sure you have all these dependences installed before moving on:

- WordPress >= 4.7
- PHP >= 7.0
- [Composer](https://getcomposer.org)
- [Node.js](https://nodejs.org)

### Understanding Starter Assumptions

Today, WordPress theme development is pretty rough. Starter aims to introduce some standardized and comfortable ways for creating advanced WordPress powered websites. However, you have to understand where it works the best. Here are some answers that can be helpful:

**Just starting the PHP and WordPress adventure?**

Probably not. It favors modern and advanced concepts. We do not discourage you but, grow as the developer and come back you will appreciate it twice.

**Creating a theme which will be widely distributed (e.g. through WordPress.org repository)?**

No. Strong reliance on modern toolsets like Composer, NPM or Webpack requires a hight web development knowledge. It wasn’t designed for casual use in mind.

**Creating an advanced website, which will be continuously developed?**

Definitely. Better organization, readable structures, patterns and modern principles. Your team will love it, just dig in into the documentation.
