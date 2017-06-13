---
extends: docs
title: "Handling translations"
group: "Basics"
subgroup: "Setup"
---

It is better to make your theme multilanguage ready. To help you with that starter comes preconfigured and ready for translating.

Your translation `.po` and `.mo` files should be stored in `resources/languages` directory.

## Configuration

Translations are loaded by `load_textdomain()` function inside `app/Setup/support.php` component.

Project textdomain string can be configured inside `config/app.php` file with `textdomain` option.

## Translation Strings

When project translations are properly loaded you can start making your theme multilanguage ready. You can retrieve sentences from language files using the `__` gettext function.

<pre class="pre"><code class="language-php">echo __('Hello world!')</code></pre>

Note! Instead of explicitly entering your project textdomain string you should take advantage of theme configuration. Use [`config()`]() helper function to pull textdomain directly from `config/app.php` file.

<pre class="pre"><code class="language-php">use function App\Theme\config;

echo __('Hello world!', config('textdomain'))</code></pre>

## Translating

Inside `resources/languages` directory you will find `tonik.pot`. This is a template file for your new translation. Open it with an editor of your choice (like [Poedit](https://poedit.net/)) and translate available sentences.
