---
title: Clearing the Cache Dynamically
categories: tutorials
tags: clearing-the-cache
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/35
---

ZenCache automatically handles updating the cache in many scenarios, such as when you publish a new post, or when you change your WordPress theme. However, there are many scenarios where you need to have finer control over when the cache is cleared, such as when a plugin or theme does not include support for WordPress caching plugins.

The following examples use the [WordPress API hooks and filters](http://codex.wordpress.org/Plugin_API) system to call a custom function that will clear the cache when a specific event occurs. 

You can call any class method that is declared as a public function in `zencache.inc.php` or `zencache-pro.inc.php` using `$GLOBALS['zencache']->any_public_method()`.

Note that while you can add this code to your theme's `functions.php` file or use a [Functionality Plugin](https://wordpress.org/plugins/functionality/), we recommend using a [WordPress Must-Use Plugin](http://codex.wordpress.org/Must_Use_Plugins) by creating a file like `wp-content/mu-plugins/zc-clear-cache.php` and then adding the necessary PHP code (note that if the `mu-plugins` directory doesn't exist, you should create it).

What follows are a few examples of how you can clear the cache dynamically.

## Clear entire cache when saving any post

If you want to clear the cache every time a post is saved or updated (i.e., when the `save_post` action is fired), you can use the following:

```php
add_action( 'save_post', 'my_custom_purge_cache', 10, 1 );

function my_custom_purge_cache( ) {
    $GLOBALS['zencache']->clear_cache();
}
```

## Clear page cache when Custom Post Type is saved

Using the `save_post_{$post_type}` hook, which is fired whenever that custom post type is created or updated (see [docs](http://codex.wordpress.org/Plugin_API/Action_Reference/save_post)), you can use something like the following to clear the cache for a given page whenever a post with that custom post type is saved:

```php
add_action( 'save_post_my-custom-post-type', 'clear_cache_for_page_id_5', 10, 1 );

function clear_cache_for_page_id_5( ) {
	$GLOBALS['zencache']->auto_clear_post_cache(5);
}
```

You'll want to change `5` to the ID of the Page/Post whose cache you'd like to clear when that custom post type is saved, and you'll want to change `my-custom-post-type` to the actual name of your Custom Post Type.

## Clear a specific page cache when saving any post

Using the `save_post` hook, which is fired whenever a post created or updated (see [docs](http://codex.wordpress.org/Plugin_API/Action_Reference/save_post)), you can use something like the following to clear the cache for a given page:

```php
add_action( 'save_post', 'clear_cache_for_page_id_5', 10, 1 );

function clear_cache_for_page_id_5( ) {
	$GLOBALS['zencache']->auto_clear_post_cache(5);
}
```

You'll want to change `5` to the ID of the Page/Post whose cache you'd like to clear.

## Clear the cache for a Logged-In User (when caching for Logged-In Users is enabled)

To clear the cache for a specific user by passing the User ID, you can use the following to, for example, clear the cache for the user with User ID `25`:

```php
add_action( 'init', 'clear_user_cache_for_id_25', 10, 1 );

function clear_user_cache_for_id_25( ) {
	$GLOBALS['zencache']->auto_clear_user_cache(25);
}
```

You'll want to change `25` to the User ID whose cache you'd like to clear.

If you just want to clear the cache for the currently logged in user, you can use the following code instead (this uses `get_current_user_id()` to detect the User ID of the current user):

```php
add_action( 'init', 'clear_current_user_cache', 10, 1 );

function clear_current_user_cache( ) {
	$GLOBALS['zencache']->auto_clear_user_cache_cur();
}
```