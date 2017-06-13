---
extends: docs
title: "Config"
group: "Architecture"
---

The `Tonik\Gin\Foundation\Config` class provides a simple way for creating flexible data collections. It implements the `ArrayAccess` interface so you can iterate on it as on a standard array.

## Usage

#### Initializing config

Pass an array of options on class initialization.

<pre class="pre"><code class="language-php">use Tonik\Gin\Foundation\Config;

$config = new Config(['textdomain' => 'theme-textdomain']);

// $config: class Tonik\Gin\Foundation\Config()</code></pre>

#### Getting all configuration values as an array

If you want to get a standard array with your configuration options, call `all` method or directly cast config variable to an array.

<pre class="pre"><code class="language-php">$config->all();
(array) $config;

// ['textdomain' => 'theme-textdomain']</code></pre>

#### Getting single configuration values

You can get a single configuration value with `get` method and option name as the argument.

<pre class="pre"><code class="language-php">$config->get('textdomain');
$config['textdomain'];

// 'theme-textdomain'</code></pre>

#### Setting single configuration values

You may also set configuration options after creating. Run `set` method with the option name to update as a first argument and new value as second.

<pre class="pre"><code class="language-php">$config->set('textdomain', 'new-textdomain');
$config['textdomain'] = 'new-textdomain';

// ['textdomain' => 'new-textdomain']</code></pre>

#### Checking whether there an entry in configuration

The `has` method verifies if an option exists in the configuration.

<pre class="pre"><code class="language-php">$config->has('textdomain');   // true
$config->has('missing');      // false

isset($config['textdomain']); // true
isset($config['missing']);    // false</code></pre>

## Filters

#### `tonik/gin/config/get/{option}`

Allows for modifying a configuration value of the specific option on getting.

<pre class="pre"><code class="language-php">add_filter('tonik/gin/config/get/key', function($value) {
    return ucfirst($value);
});</code></pre>

#### `tonik/gin/config/set/{option}`

Allows for modifying a configuration value of the specific option when setting.

<pre class="pre"><code class="language-php">add_filter('tonik/gin/config/set/key', function($value) {
    return ucfirst($value);
});</code></pre>
