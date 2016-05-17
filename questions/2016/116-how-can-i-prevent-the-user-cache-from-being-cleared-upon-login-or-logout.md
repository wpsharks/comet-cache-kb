---
title: How can I prevent the user cache from being cleared upon login or logout?
categories: questions
tags: logged-in-users, mu-plugins-hacks, clearing-the-cache
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/116
---

When caching for Logged-In Users is enabled, Comet Cache will automatically clear the users cache whenever they login or logout (see [this article](https://cometcache.com/r/kb-article-why-is-the-user-cache-cleared-when-a-post-occurs/) for why). If you want to override this behavior, you can use an [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins).

_Note: The example below assumes that users are logging in via the WordPress login page (`wp-login.php`) and logging out using the logout link in the WordPress Toolbar. If you have a login widget or another way of logging in and out, you may need to adjust the example below to work with your site._

Create this file and directory:
`wp-content/mu-plugins/cc-logged-in-users.php`

```php
<?php
/*
Plugin Name: Disable Comet Cache Logged-In User Cache Clearing on Login/Logout
Description: Disables the automatic Comet Cache routines that clear the user cache upon login/logout when caching for Logged-In Users is enabled
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://cometcache.com.
*/

add_filter('comet_cache_invalidate_when_logged_in_postload', function ($invalidate) {
    if (empty($_REQUEST)) { // i.e., no GET/POST vars?
        return $invalidate; // Nothing to do here.
    }
    $request_uri = !empty($_SERVER['REQUEST_URI']) ? $_SERVER['REQUEST_URI'] : '';
    $is_wp_login_php = mb_strpos($request_uri, '/wp-login.php') !== false;
    $action = !empty($_REQUEST['action']) ? $_REQUEST['action'] : ($is_wp_login_php ? 'login' : '');

    if ($is_wp_login_php && in_array($action, ['login', 'logout'], true)) {
        return $invalidate = false; // Not on this action.
    } else {
        return $invalidate; // What CC says.
    }
});
```
