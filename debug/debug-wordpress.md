# Debugging in WordPress

Debugging PHP code is part of any project, but WordPress comes with specific debug systems designed to simplify the process as well as standardize code across the core, plugins and themes. This page describes the various debugging tools in WordPress and how to be more productive in your coding as well as increasing the overall quality and interoperativity of your code.

For non-programmers or general users, these options can be used to show detailed information about errors.

## [Example wp-config.php for Debugging](#example-wp-config-php-for-debugging)

The following code, inserted in your [wp-config.php](/support/article/editing-wp-config-php/) file, will log all errors, notices, and warnings to a file called debug.log in the wp-content directory. It will also hide the errors so they do not interrupt page generation.

```
// Enable WP\_DEBUG mode
define( 'WP\_DEBUG', true );
```

```
// Enable Debug logging to the /wp-content/debug.log file
define( 'WP\_DEBUG\_LOG', true );
```

```
// Disable display of errors and warnings
define( 'WP\_DEBUG\_DISPLAY', false );
@ini\_set( 'display\_errors', 0 );
```

```
// Use dev versions of core JS and CSS files (only needed if you are modifying these core files)
define( 'SCRIPT\_DEBUG', true );
```

**NOTE**: You must insert this **BEFORE** `/* That's all, stop editing! Happy blogging. */` in the [wp-config.php](/support/article/editing-wp-config-php/) file.

## [WP\_DEBUG](#wp_debug)

`WP_DEBUG` is a PHP constant (a permanent global variable) that can be used to trigger the “debug” mode throughout WordPress. It is assumed to be false by default and is usually set to true in the [wp-config.php](/support/article/editing-wp-config-php/) file on development copies of WordPress.

```
// This enables debugging.
define( 'WP\_DEBUG', true );
```

```
// This disables debugging.  
define( 'WP\_DEBUG', false );
```

**Note**: The `true` and `false` values in the example are not surrounded by apostrophes (‘) because they are boolean (true/false) values. If you set constants to `'false'`, they will be interpreted as true because the quotes make it a string rather than a boolean.

It is not recommended to use `WP_DEBUG` or the other debug tools on live sites; they are meant for local testing and staging installs.

### [PHP Errors, Warnings, and Notices](#php-errors-warnings-and-notices)

Enabling `WP_DEBUG` will cause all PHP errors, notices and warnings to be displayed. This is likely to modify the default behavior of PHP which only displays fatal errors and/or shows a white screen of death when errors are reached.

Showing all PHP notices and warnings often results in error messages for things that don’t seem broken, but do not follow proper data validation conventions inside PHP. These warnings are easy to fix once the relevant code has been identified, and the resulting code is almost always more bug-resistant and easier to maintain.

### [Deprecated Functions and Arguments](#deprecated-functions-and-arguments)

Enabling `WP_DEBUG` will also cause notices about deprecated functions and arguments within WordPress that are being used on your site. These are functions or function arguments that have not been removed from the core code yet but are slated for deletion in the near future. Deprecation notices often indicate the new function that should be used instead.

## [WP\_DEBUG\_LOG](#wp_debug_log)

`WP_DEBUG_LOG` is a companion to WP\_DEBUG that causes all errors to also be saved to a debug.log log file This is useful if you want to review all notices later or need to view notices generated off-screen (e.g. during an AJAX request or wp-cron run).

Note that this allows you to write to log file using PHP’s built in `error_log()` function, which can be useful for instance when debugging Ajax events.

When set to `true`, the log is saved to `debug.log` in the content directory (usually `wp-content/debug.log`) within your site’s filesystem. Alternatively, you can set it to a valid file path to have the file saved elsewhere.

```
define( 'WP\_DEBUG\_LOG', true );
```
-or-
```
define( 'WP\_DEBUG\_LOG', '/tmp/wp-errors.log' );
```

**Note**: for `WP_DEBUG_LOG` to do anything, `WP_DEBUG` must be enabled (true). Remember you can turn off `WP_DEBUG_DISPLAY` independently.

## [WP\_DEBUG\_DISPLAY](#wp_debug_display)

`WP_DEBUG_DISPLAY` is another companion to `WP_DEBUG` that controls whether debug messages are shown inside the HTML of pages or not. The default is ‘true’ which shows errors and warnings as they are generated. Setting this to false will hide all errors. This should be used in conjunction with `WP_DEBUG_LOG` so that errors can be reviewed later.

```
define( 'WP\_DEBUG\_DISPLAY', false );
```

**Note**: for `WP_DEBUG_DISPLAY` to do anything, `WP_DEBUG` must be enabled (true). Remember you can control `WP_DEBUG_LOG` independently.

## [SCRIPT\_DEBUG](#script_debug)

`SCRIPT_DEBUG` is a related constant that will force WordPress to use the “dev” versions of core CSS and JavaScript files rather than the minified versions that are normally loaded. This is useful when you are testing modifications to any built-in .js or .css files. Default is false.

```
define( 'SCRIPT_DEBUG', true );
```

## [SAVEQUERIES](#savequeries)

The `SAVEQUERIES` definition saves the database queries to an array and that array can be displayed to help analyze those queries. The constant defined as true causes each query to be saved, how long that query took to execute, and what function called it.

```
define( 'SAVEQUERIES', true );
```

The array is stored in the global `$wpdb->queries`.

**NOTE**: This will have a performance impact on your site, so make sure to turn this off when you aren’t debugging.

## [Debugging Plugins](#debugging-plugins)

There are many [debugging plugins](https://wordpress.org/plugins/search.php?q=debug) for WordPress that show more information about the internals, either for a specific component or in general. Here are some examples:

* [Query Monitor](https://wordpress.org/plugins/query-monitor/)
* [Debug Bar](https://wordpress.org/plugins/debug-bar/)
* [Log Deprecated Notices](https://wordpress.org/plugins/log-deprecated-notices/)

## [External Resources](#external-resources)

* [WordPress ‘wp-config.php’ file Generator](http://generatewp.com/wp-config/)
* [‘No White Screen’ plugin: Display the error instead of a white screen](https://github.com/stracker-phil/wp-no-white-screen/)

## Changelog

- 2022-09-04: Created from [Debugging in WordPress](https://wordpress.org/support/article/debugging-in-wordpress/) ticket from [Github](https://github.com/WordPress/Documentation-Issue-Tracker/issues/349)
