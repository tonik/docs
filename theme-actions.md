---
extends: docs
title: "Theme actions"
group: "Basics"
subgroup: "Setup"
prev: defining-ajax-responses
next: theme-filters
order: 1
---

Actions allow you to trigger various logic at the specific moments and places when executing your application.

They should be registered inside `app/Setup/actions.php` file. As a simple example, let's output `Hello World` to the footer.

```php
namespace Tonik\Theme\App\Setup;

function render_text()
{
  echo "Hello world!";
}
add_action('wp_footer', 'Tonik\Theme\App\Setup\render_text');
```

## Examples

### Using action to reconfigure PHPMailer to use SMTP

```php
namespace Tonik\Theme\App\Setup;

function recofigure_phpmailer_to_smtp($phpmailer)
{
    $phpmailer->isSMTP();
    $phpmailer->Host = 'host';
    $phpmailer->SMTPAuth = true;
    $phpmailer->Port = 2525;
    $phpmailer->Username = 'username';
    $phpmailer->Password = 'password';
}
add_action('phpmailer_init', 'Tonik\Theme\App\Setup\swap_mail_to_use_mailtrap');
```