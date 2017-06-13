---
extends: docs
title: "Theme Service Container"
group: "Architecture"
---

The `Tonik\Gin\Foundation\Theme` class is a backbone of the theme which performs the services container role. It utilizes a [singleton pattern](//en.wikipedia.org/wiki/Singleton_pattern), so every time you initiate it you will receive the same object.

## Usage

### Initializing theme container

<pre class="pre"><code class="language-php">use Tonik\Gin\Foundation\Theme;

$theme = new Theme;</code></pre>

### Binding services in the container

To bind a value inside container simply call `bind` or `factory` method with a binding name as the first parameter. The second argument should be a closure which returns desired value.

<pre class="pre"><code class="language-php">$theme->bind('basic', function() {
    return 'value';
});</code></pre>

Inside closure callback, you have access to the two parameters. First is an instance of `Tonik\Gin\Foundation\Theme`, second are variables passed on service resolving.

<pre class="pre"><code class="language-php">$theme->bind('basic/parameters', function(Theme $theme, $parameters) {
    // $theme: class Tonik\Gin\Foundation\Theme
    // $parameters: ['key' => 'value']
});

// Resolve service with parameter.
$theme->get('basic/parameters', ['key' => 'value']);</code></pre>

#### Binding singletons

Use `bind` method to create singleton service. You will receive the same instance of service every time you resolve it from the container.

<pre class="pre"><code class="language-php">use Tonik\Gin\Foundation\Config;

$theme->bind('singleton', function() {
    return new Config(['option' => 'value']);
});</code></pre>

#### Binding factories

The `factory` method allows you to create service which returns you a new instance on every resolving.

<pre class="pre"><code class="language-php">$theme->factory('service', function () {
    return new Config(['option' => 'value']);
});</code></pre>

### Resolving services from the container

Run `get` method with service name as an argument to resolve previously bounded value out of the container.

<pre class="pre"><code class="language-php">$theme->get('service');</code></pre>

You can also resolve services which are requiring some sort of parameter.

<pre class="pre"><code class="language-php">$theme->get('basic/parameters', ['key' => 'value']);</code></pre>

### Checking for bonded service

You may want to check if service is already bounded inside the container. Use `has` method and service name as a parameter.

<pre class="pre"><code class="language-php">$theme->has('service');</code></pre>

### Removing service from the container

Call `forget` to remove previously bounded service inside the container.

<pre class="pre"><code class="language-php">$theme->forget('service');</code></pre>
