---
extends: docs
title: "Template"
group: "Architecture"
---

The `Tonik\Gin\Template\Template` class provides a fluent API for working with theme template files.

## Usage

### Initializing template

Template class requires the `Tonik\Gin\Foundation\Config` instance to be injected with `templates`, `paths` and `directories` properties setup.

<pre class="pre"><code class="language-php">use Tonik\Gin\Template\Template;
use Tonik\Gin\Foundation\Config;

$config = new Config([
    'templates' => [
        'extension' => '.tpl.php'
    ],
    'paths' => [
        'directory' => get_template_directory(),
    ],
    'directories' => [
        'templates' => 'resources/templates'
    ]
]);

$template = new Template($config);</code></pre>

Now you can set template file path as relative to the `resources/templates` directory.

<pre class="pre"><code class="language-php">// resources/templates/content.tpl.php
$template->setFile('content');</code></pre>

By passing an array of two names, you can set variance of the template. This mechanism is borrowed directly form [`get_template_part()`](https://developer.wordpress.org/reference/functions/get_template_part/) function. Visit codex for more details.

<pre class="pre"><code class="language-php">// resources/templates/content-empty.tpl.php
$template->setFile(['content', 'empty']);</code></pre>

### Getting template relative path

Gets template path relatively to the project root directory.

<pre class="pre"><code class="language-php">$template->getRelativePath();

// 'resources/templates/content.tpl.php'</code></pre>

### Getting template directory path

Gets full directory path to the template on your server.

<pre class="pre"><code class="language-php">$template->getPath();

// 'website/directory/resources/templates/button.tpl.php'</code></pre>

### Rendering template

A template can be outputted with `render` method.

<pre class="pre"><code class="language-html"><!-- @ resources/templates/content.tpl.php -->
<main>Lorem ipsum.</main></code></pre>
<pre class="pre"><code class="language-php">$template->render();</code></pre>

Of course, you can pass various data to the template with an associative array as the method argument. Key will become a variable name.

<pre class="pre"><code class="language-html"><!-- @ resources/templates/content.tpl.php -->
<main><?= $title =></main></code></pre>
<pre class="pre"><code class="language-php">$template->render(['text' => 'Lorem ipsum.']);</code></html>

## Filters

#### `tonik/gin/template/filename`

Allows for changing filenames of templates on rendering run.

<pre class="pre"><code class="language-php">add_filter('tonik/gin/template/filename', function($name) {
    if ($name === 'button.php') {
       return 'button-changed.php';
    }
});</code></pre>

#### `tonik/gin/template/context/{template}`

Filter for changing values of passed context of a specified template on rendering. The `{template}` section is dynamic and should take the value of a template relative path in `resources/templates` directory.

<pre class="pre"><code class="language-php">add_filter('tonik/gin/template/context/button.php', function($context) {
    $context['title'] = 'New title!';

    return $context;
});</code></html>
