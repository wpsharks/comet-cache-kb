---
title: Clearing the Cache Dynamically
categories: tutorials
tags: clearing-the-cache, mu-plugins-hacks, themeplugin-developers
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/35
---

Comet Cache automatically handles updating the cache in many scenarios, such as when you publish a new post, or when you change your WordPress theme. However, there may be scenarios where you need to have finer control over when the cache is cleared, such as when a plugin or theme does not include support for WordPress caching plugins.

The following examples use the [WordPress API hooks and filters](http://codex.wordpress.org/Plugin_API) system to call a custom function that will interface with Comet Cache to clear the cache when a specific event occurs.

Using the technique described here, you can call any class method that is declared as a public function in `comet-cache.inc.php` (Comet Cache Lite) or `src/includes/classes/ApiBase.php` (Comet Cache Pro) using `$GLOBALS['comet_cache']->any_public_method()`.

### How to use the code examples

While you can add this code to your theme's `functions.php` file or use a [Functionality Plugin](https://wordpress.org/plugins/functionality/), we recommend using a [WordPress Must-Use Plugin](http://codex.wordpress.org/Must_Use_Plugins) by creating a file like `wp-content/mu-plugins/zc-clear-cache.php` and then adding the necessary PHP code (note that if the `mu-plugins` directory doesn't exist, you should create it).

What follows are a few examples of how you can clear the cache dynamically.

## Examples using WordPress Hooks/Filters API

### Clear entire cache when saving any post

If you want to clear the cache every time a post is saved or updated (i.e., when the `save_post` action is fired), you can use the following.

**Comet Cache Lite**

```php
add_action( 'save_post', 'my_custom_clear_cache', 10, 1 );

function my_custom_clear_cache( ) {
    $GLOBALS['comet_cache']->clear_cache();
}
```

**Comet Cache Pro**

```php
add_action( 'save_post', 'my_custom_clear_cache', 10, 1 );

function my_custom_clear_cache( ) {
    $GLOBALS['comet_cache']->clearCache();
}
```

### Clear page cache when Custom Post Type is saved

Using the `save_post_{$post_type}` hook, which is fired whenever that custom post type is created or updated (see [docs](http://codex.wordpress.org/Plugin_API/Action_Reference/save_post)), you can use something like the following to clear the cache for a given page whenever a post with that custom post type is saved.

**Comet Cache Lite**

```php
add_action( 'save_post_my-custom-post-type', 'clear_cache_for_page_id_5', 10, 1 );

function clear_cache_for_page_id_5( ) {
	$GLOBALS['comet_cache']->auto_clear_post_cache(5);
}
```
You'll want to change `5` to the ID of the Page/Post whose cache you'd like to clear when that custom post type is saved, and you'll want to change `my-custom-post-type` to the actual name of your Custom Post Type.

**Comet Cache Pro**

```php
add_action( 'save_post_my-custom-post-type', 'clear_cache_for_page_id_5', 10, 1 );

function clear_cache_for_page_id_5( ) {
	$GLOBALS['comet_cache']->autoClearPostCache(5);
}
```

You'll want to change `5` to the ID of the Page/Post whose cache you'd like to clear when that custom post type is saved, and you'll want to change `my-custom-post-type` to the actual name of your Custom Post Type.

### Clear a specific page cache when saving any post

Using the `save_post` hook, which is fired whenever a post created or updated (see [docs](http://codex.wordpress.org/Plugin_API/Action_Reference/save_post)), you can use something like the following to clear the cache for a given page.

**Comet Cache Lite**

```php
add_action( 'save_post', 'clear_cache_for_page_id_5', 10, 1 );

function clear_cache_for_page_id_5( ) {
	$GLOBALS['comet_cache']->auto_clear_post_cache(5);
}
```

You'll want to change `5` to the ID of the Page/Post whose cache you'd like to clear.

**Comet Cache Pro**

```php
add_action( 'save_post', 'clear_cache_for_page_id_5', 10, 1 );

function clear_cache_for_page_id_5( ) {
	$GLOBALS['comet_cache']->autoClearPostCache(5);
}
```

You'll want to change `5` to the ID of the Page/Post whose cache you'd like to clear.

### Clear the cache for a Logged-In User (when caching for Logged-In Users is enabled)

To clear the cache for a specific user by passing the User ID, you can use the following. The examples below clear the cache for the user with User ID `25`.

**Comet Cache Lite**

```php
add_action( 'init', 'clear_user_cache_for_id_25', 10, 1 );

function clear_user_cache_for_id_25( ) {
	$GLOBALS['comet_cache']->auto_clear_user_cache(25);
}
```

You'll want to change `25` to the User ID whose cache you'd like to clear.

**Comet Cache Pro**

```php
add_action( 'init', 'clear_user_cache_for_id_25', 10, 1 );

function clear_user_cache_for_id_25( ) {
	$GLOBALS['comet_cache']->autoClearUserCache(25);
}
```

You'll want to change `25` to the User ID whose cache you'd like to clear.

### Clear the cache for the currently Logged-In User (when caching for Logged-In Users is enabled)

If you just want to clear the cache for the currently logged in user, you can use the following code (this uses `get_current_user_id()` to detect the User ID of the current user).

**Comet Cache Lite**

```php
add_action( 'init', 'clear_current_user_cache', 10, 1 );

function clear_current_user_cache( ) {
	$GLOBALS['comet_cache']->auto_clear_user_cache_cur();
}
```

**Comet Cache Pro**

```php
add_action( 'init', 'clear_current_user_cache', 10, 1 );

function clear_current_user_cache( ) {
	$GLOBALS['comet_cache']->autoClearUserCacheCur();
}
```

## Using the Comet Cache API Class

If you need to call the Comet Cache API from another PHP file, you'll probably want to use the Comet Cache API Class. This will require first loading the WordPress framework (via `wp-load.php`).

### Comet Cache Lite

```php
<?php
// Load WordPress framework
require_once dirname(__FILE__).'/wp-load.php';

// Any of these API calls can now be made from this PHP file
comet_cache::version();
comet_cache::options();
comet_cache::clear();
comet_cache::wipe();
comet_cache::purge();
```

### Comet Cache Pro

```php
<?php
// Load WordPress framework
require_once dirname(__FILE__).'/wp-load.php';

// Any of these API calls can now be made from this PHP file
comet_cache::version();
comet_cache::options();
comet_cache::clear();
comet_cache::wipe();
comet_cache::purge();
comet_cache::clearPost($post_id);
comet_cache::clearUser($user_id);
comet_cache::clearCurrentUser();
comet_cache::clearUrl($url);
```
