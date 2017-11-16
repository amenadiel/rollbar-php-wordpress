# Rollbar for WordPress
[![Plugin Version](https://img.shields.io/wordpress/plugin/v/rollbar.svg)](https://wordpress.org/plugins/rollbar/) [![WordPress Version Compatibility](https://img.shields.io/wordpress/v/rollbar.svg)](https://wordpress.org/plugins/rollbar/) [![Downloads](https://img.shields.io/wordpress/plugin/dt/rollbar.svg)](https://wordpress.org/plugins/rollbar/) [![Rating](https://img.shields.io/wordpress/plugin/r/rollbar.svg)](https://wordpress.org/plugins/rollbar/)

Rollbar full-stack error tracking for WordPress

## Description
Rollbar collects errors that happen in your application, notifies you, and analyzes them so you can debug and fix them.

This plugin integrates Rollbar into your WordPress installation.

Find out [how Rollbar can help you decrease development and maintenance costs](https://rollbar.com/features/).

See [real companies improving their development workflow thanks to Rollbar](https://rollbar.com/customers/).

[Official WordPress.org Plugin](https://wordpress.org/plugins/rollbar/)

## Installation

### Through [WordPress Plugin directory](https://wordpress.org/plugins/rollbar/)

The easiest way to install the plugin is from the WordPress Plugin directory. If you have an existing WordPress installation and you want to add Rollbar:

1. In your WordPress administration panel go to `Plugins` → `Add New`.
2. Search for "Rollbar" and find `Rollbar` by Rollbar in the search results.
3. Click `Install Now` next to the `Rollbar` plugin.
4. In `Plugins` → `Installed plugins` find `Rollbar` and click `activate` underneath.
5. Log into your [Rollbar account dashboard](https://rollbar.com/login/).
6. Go to `Settings` → `Project Access Tokens`.
7. Copy the token value under `post_client_item` and `post_server_item`.
8. Navigate to `Tools` → `Rollbar`.
9. Enable `PHP error logging` and/or `Javascript error logging` depending on your needs.
10. Paste the tokens you copied in step 7 in `Access Token` section.
11. Provide the name of your environment in `Environment`. By default, the environment will be taken from `WP_ENV` environment variable if it's set otherwise it's blank. We recommend to fill this out either with `development` or `production`.
12. Pick a minimum logging level. Only errors at that or higher level will be reported. For reference: [PHP Manual: Predefined Error Constants](http://php.net/manual/en/errorfunc.constants.php).
13. Click `Save Changes`.

**Warning**: This installation method might not be suitable for complex WordPress projects. The plugin installed this way will be self-contained and include all of the required dependencies for itself and `rollbar/rollbar-php` library. In complex projects, this might lead to version conflicts between dependencies and other plugins/packages. If this is an issue in your project, we recommend the "Advanced" installation method. For more information why this might be important for you, read [Using Composer with WordPress](https://roots.io/using-composer-with-wordpress/).

### Through [wpackagist](https://wpackagist.org/) (if you manage your project with Composer) *recommended*

This is a recommended way to install Rollbar plugin for advanced projects. This way ensures the plugin and all of its' dependencies are managed by Composer.

1. If your WordPress project is not managed with Composer yet, we suggest looking into upgrading your WordPress: [Using Composer with WordPress](https://roots.io/using-composer-with-wordpress/).
2. In your `composer.json` add `wpackagist-plugin/rollbar` to your `require` section, i.e.:
```
  "require": {
    "php": ">=5.5",
    ...,
    "wpackagist-plugin/rollbar": "*"
  }
```
3. Issue command `composer install` in the root directory of your WordPress project.
4. In `Plugins` → `Installed plugins` find `Rollbar` and click `Activate` underneath.
5. Log into your [Rollbar account dashboard](https://rollbar.com/login/).
6. Go to `Settings` → `Project Access Tokens`.
7. Copy the token value under `post_client_item` and `post_server_item`.
8. Navigate to `Tools` → `Rollbar`.
9. Enable `PHP error logging` and/or `Javascript error logging` depending on your needs.
10. Paste the tokens you copied in step 7 in `Access Token` section.
11. Provide the name of your environment in `Environment`. By default, the environment will be taken from `WP_ENV` environment variable if it's set otherwise it's blank.
12. Pick a minimum logging level. Only errors at that or higher level will be reported. For reference: [PHP Manual: Predefined Error Constants](http://php.net/manual/en/errorfunc.constants.php).
13. Click `Save Changes`.

## Configuration

### `rollbar_js_config` filter

Allows a plugin to modify the JS config passed to Rollbar.

You can use this e.g. to add the currently logged in user to the `person` field
of the payload. With this change, you could have this plugin:

```php
class RollbarWPUser {

  public function __construct(){
    add_filter( 'rollbar_js_config', array($this, 'rollbar_js_config') );
  }

  function rollbar_js_config($config) {
    if(is_user_logged_in()) {
      $user = wp_get_current_user();  
      
      if(empty($config['payload']['person'])) {
        $config['payload']['person'] = array(
          'id' => $user->ID,
          'username' => $user->user_login,
          'email' => $user->user_email
        );
      }
    }

    return $config;
  }
  
}
```

## Help / Support

If you run into any issues, please email us at [support@rollbar.com](mailto:support@rollbar.com)

You can also find us on IRC: [#rollbar on chat.freenode.net](irc://chat.freenode.net/rollbar)

For bug reports, please [open an issue on GitHub](https://github.com/rollbar/rollbar-php-wordpress/issues/new).

## Special thanks

The original author of this package is [@flowdee](https://twitter.com/flowdee/). This is a fork and continuation of his efforts.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Testing
*Note:* Before you run `composer test`, make sure your mysql instance is running and the following are correct credentials:
Test database: wordpress_test
Test db username: root 
Test db password: '' 
Test db host: localhost

Tests are in `tests`.
To run the tests: `composer test`
To fix code style issues: `composer fix`

## Disclaimer

This plugin is a community-driven contribution. All rights reserved to Rollbar. 

[![Rollbar](https://d26gfdfi90p7cf.cloudfront.net/rollbar-badge.144534.o.png)](https://rollbar.com/)
