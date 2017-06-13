---
extends: docs
title: "Autoloader"
group: "Architecture"
---

The `Tonik\Gin\Foundation\Autoloader` class helps with autoloading theme components files.

## Usage

### Initializing autoloader

Autoloader class requires instance of `Tonik\Gin\Foundation\Config` to be injected with setup `paths`, `directories` and `autoload` properties. The `autoload` option should include list of component relative to the `app/` directory paths.

<pre class="pre"><code class="language-php">use Tonik\Gin\Foundation\Config;
use Tonik\Gin\Foundation\Autoloader;

$config = new Config([
    'paths' => [
        'directory' => get_template_directory(),
    ],
    'directories' => [
        'app' => 'app',
    ],
    'autoload' => [
        'Http/assets.php',
    ]
]);

$autoloader = new Autoloader($config);</code></pre>

### Requiring components listed to autoload

To autoload listed component simply call `load` method. This will `require_once` all listed files.

<pre class="pre"><code class="language-php">$autoloader->load();</code></pre>

### Getting relative path of autoloaded component

Gets path of a specified component relatively to the project `app` directory.

<pre class="pre"><code class="language-php">$autoloader->getRelativePath('Http/assets.php');

// 'app/Http/assets.php'</code></pre>

### Getting path of autoloaded component

Gets full directory path to the component file on your server.

<pre class="pre"><code class="language-php">$autoloader->getPath('Http/assets.php');

// 'website/directory/app/Http/assets.php'</code></pre>

## Actions

#### `tonik/gin/autoloader/before_load`

Fires before requiring listed files by autoloader.

<pre class="pre"><code class="language-php">add_action('tonik/gin/autoloader/before_load', function() {
  // logic
});</code></pre>

#### `tonik/gin/autoloader/after_load`

Fires after requiring listed files by autoloader.

<pre class="pre"><code class="language-php">add_action('tonik/gin/autoloader/after_load', function() {
  // logic
});</code></pre>
