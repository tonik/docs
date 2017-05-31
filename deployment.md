---
extends: _layouts.docs
title: "Deployment"
group: "Getting Started"
---

## Server requirements

This theme follows WordPress [recommended requirements](https://wordpress.org/about/requirements/). Your server must fulfill following requirements:

- At least PHP >= 7.0
- MySQL >=5.6 or MariaDB >=10.0
- The mod_rewrite Apache module

## Installing a Theme

Download or clone theme repository to the wp-content/themes directory.

```bash
# @ /wp-content/themes
# Clone repository to the themes folder.
$ git clone git@github.com:<repository>/<theme-name>.git <theme-name>
```

Go into theme directory and run following commands to resolve dependencies and build a theme.

```bash
# @ /wp-content/themes
# Change directory to the cloned folder.
$ cd <theme-name>

# @ /wp-content/themes/<theme-name>
# Install required composer dependences (without these needed only to development).
$ composer install -o --no-devs

# @ /wp-content/themes/<theme-name>
# Install required npm dependences for building a theme.
$ npm install
```

All files inside `public/` directory are ignored, it's recommended to not store compiled assets inside the repository. This requires us to build theme after each deploy.

```bash
# @ /wp-content/themes/<theme-name>
# Build theme assets for production.
$ npm run prod
```