---
extends: docs
title: "Using service container"
group: "Basics"
subgroup: "Setup"
prev: handling-translations
next: registering-custom-post-types
order: 5
---

The starter introduces really simple but very helpful service container for better organization and separation of your code. Let's quote some definition:

`A Service Container is a special object that manages the instantiation of services inside an application. Instead of creating services directly, the developer trains the service container (via configuration) on how to create the services.`
-- [Symfony Glossary](http://symfony.com/doc/2.0/glossary.html#term-service-container)

It sounds scary, but it is an easy concept. Let's see some examples.

## Usage

All of your bindings should be defined inside `app/Setup/services.php` file.
It's recommended to use a [`theme()`](/theme/docs/helper-functions/) helper function for operating on service container; this gives you an ability to access the container anywhere in your project components.

> Please, visit the [Theme Service Container documentation](/theme/docs/theme-service-container/) for a more detailed description about API.

#### Creating services

You should register your project bindings within a named function which is attached to the `init` action hook. This will give you a confidence that everything is booted and ready for binding.

Register your service with `theme()` helper inside the hooked function. Remember to import a proper use statement (`use function Tonik\Theme\App\theme`).

```php
namespace Tonik\Theme\App\Setup;

use function Tonik\Theme\App\theme;

function bind_service()
{
  theme()->bind('service', function() {
    return true;
  });
}
add_action('init', 'Tonik\Theme\App\Setup\bind_service');
```

#### Retrieving services

After service registration, you can also retrieve it with `theme()` helper function. Pass its name as the first parameter or use `get` method.

```php
theme('service');

theme()->get('service');
```

To resolve services with additional parameters pass associative array of key and values as the second argument.

```php
theme('service', ['key' => 'value']);
```

Now, you have access to these parameters inside service closure in second argument.

```php
theme()->bind('service', function(Theme $theme, array $parameters) {
  // $parameters: ['key' => 'value']
});
```

## Examples

### Services for database queries

Standard binding with `bind` resolves service only once and returns a deposited value on every retrieving. It's a great place for fetching entries from the database because it gives you a certainty that you are querying your database only once.

```php
namespace Tonik\Theme\App\Setup;

use function Tonik\Theme\App\theme;
use Tonik\Gin\Foundation\Theme;

/**
 * Service handler for retrieving posts of specific post type.
 *
 * @return void
 */
function bind_books_service()
{
  /**
   * Binds service for retrieving posts of specific post type.
   *
   * @param \Tonik\Gin\Foundation\Theme $theme  Instance of the service container
   * @param array $parameters  Parameters passed on service resolving
   *
   * @return \WP_Post[]
   */
  theme()->bind('books', function (Theme $theme, $parameters) {
    return new WP_Query([
      'post_type' => 'book',
    ]);
  });
}
add_action('init', 'Tonik\Theme\App\Setup\bind_books_service');
```

Now, you can simply retrieve posts of book post type anywhere in your project via registered service.

```php
$genres = theme('books');
```

However, take note that bounded services always returns deposited value after first retrieving. If you want to pass to service a dynamic parameters you probably need to register service as factory:

```php
theme()->factory('book/genres', function (Theme $theme, $parameters) {
  return wp_get_post_terms($parameters['id'], 'book_genre');
});

$genres = theme('book/genres', ['id' => get_the_ID()]);
```

### Services for external API requests

You may also define services which connect to the external resources. Use in pair with transients to achieve the best performance.

```php
namespace Tonik\Theme\App\Setup;

use function Tonik\Theme\App\theme;

/**
 * Service handler for retriving data from API.
 *
 * @return void
 */
function bind_api_endpoint_service()
{
  /**
   * Bind service for retrieving data from API.
   *
   * @return array
   */
  theme()->bind('api/endpoint', function () {
    if (false === ($response = get_transient('api/endpoint/transient'))) {
      $response = wp_remote_post("https://api.io/endpoint", [
        'body' => [
          'client_id'  => CLIENT_ID,
          'secret_key' => SECRET_KEY
        ]
      ]);

      set_transient('api/endpoint/transient', $response, DAY_IN_SECONDS);
    }

    return json_decode($response['body']);
  });
}
add_action('init', 'Tonik\Theme\App\Setup\bind_api_endpoint_service');
```

You should define APIs configuration keys as constants in the `wp-config.php` file.

```php
define('CLIENT_ID', 'client-id');
define('SECRET_KEY', 'secret-key');
```

Now, with a simple resolving, you can pull external API data.

```php
$auth = theme('api/endpoint');
```
