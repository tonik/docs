---
extends: docs
title: "Creating templates"
group: "Basics"
---

Separation of visual layer and application logic was always a problem while developing WordPress themes. The starter offers you some additional tools to solve this problem. Ability to share and pass data between divided templates give you a lot of flexibility.

## Configuration

By default template files are stored inside `resources/templates` directory. You can control it inside `config/app.php` file with `directories.templates` option.

<pre class="pre"><code class="language-php">'directories' => [
    'templates' => 'resources/templates'
]</code></pre>

You may also customize extension of template files. By default, it is `.tpl.php`, however feel free to change it as you like in configuration file with `templates.extension` option.

<pre class="pre"><code class="language-php">'templates' => [
    'extension' => '.tpl.php'
]</code></pre>

## Usage

It is recommended to use [`template()`]() helper function to render your project template files. Let's take a look at the introductory example:

#### 1. Create view the `.tpl.php` file inside project templates directory.

<pre class="pre"><code class="language-html"><button><?= $title ?></button></code></pre>

#### 2. Render template with context using a `template()` function.

> Visit the [Template]() documentations for more completed API guides.

<pre class="pre"><code class="language-php">template('button', ['title' => 'Click me!']);</code></pre>

You can expect this output:

<pre class="pre"><code class="language-html"><button>Click me!</button></code></pre>

## Examples

Managing templates rendering with hooks is a great way for creating a reusable and easy to maintain visual layer of your theme.

### Rendering theme's single post view with help of hooks

Start with creating a template view for a single post. It is a standard loop with our custom `theme/single/content` action inside. Later, we will hook up to that action and render the content of a post.

<pre class="pre"><code class="language-html"><!-- @ resources/templates/single.tpl.php -->

<?php if (have_posts()) : ?>
    <main>
        <?php while (have_posts()) : the_post() ?>
            <?php do_action('theme/single/content') ?>
        <?php endwhile ?>
    </main>
<?php endif ?></code></pre>

Inside the `single.php` controller file, we will simply render a template created above.

<pre class="pre"><code class="language-php">// @ single.php

use function App\Theme\template;

template('single');</code></pre>

We can proceed and create a view file for a post content.

<pre class="pre"><code class="language-html"><!-- @ resources/templates/partials/content.tpl.php -->

<article>
    <header>
        <h1><?php the_title() ?></h1>
    </header>

    <p><?php the_content() ?></p>
</article></code></pre>

Now, we can hook to a `theme/single/content` action, which are executed inside `single.tpl.php` file, and render previously created template for post content.

<pre class="pre"><code class="language-php">// @ app/Setup/actions.php

function render_post_content()
{
    template('partials/post/content');
}
add_action('theme/single/content', 'App\Theme\Setup\render_post_content');</code></pre>

Nothing blocks you from hooking template rendering handler to multiple actions. This allows you to reuse various template blocks, keep logic separation and still stay DRY. Great!
