---
title: Disabling Automatic Clear / Wipe Cache Routines
categories: tutorials
tags: clearing-the-cache, mu-plugins-hacks
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/25
---

_Note: This is a [Comet Cache Pro](http://cometcache.com/prices/) feature._

If you're running a very large site with _many_ cache files, you may want manual control over when the cache is cleared or wiped. You can disable the Clear and Wipe cache routines using an [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins).

An MU-Plugin is always active and does not require activation. As soon as a plugin file is created in the `mu-plugins` directory, the MU-Plugin is immediately active and the only way to disable it is to delete the plugin file from the `mu-plugins` directory.

Please create the `wp-content/mu-plugins/` directory if it does not already exist and then add one of the following PHP files to that directory.

**Note:** These MU-Plugins only disable the automatic routines; the manual Clear Cache button, and the Wipe Cache button in MultiSite environments, still function from the WordPress Dashboard as expected. Also, auto-purge routines still function as expected; i.e., cache files for a Page/Post are still purged when the Page/Post is updated, along with any associated cache files (e.g., Home Page cache file, Posts Page cache file, Category/Tag/Author archive view cache files, etc.).

**WARNING: Disabling these automatic routines is not recommended. The following MU-Plugins should only be used by advanced site owners who understand the implications of disabling these automatic routines and who are able to take manual intervention when the cache should be cleared or wiped.**

## Disabling 'Clear Cache' Routines

Inside `wp-content/mu-plugins/` create this file: `zc-disable-auto-clear-cache-routines.php`:

```php
<?php
/*
Plugin Name: Disable Comet Cache Clear Routines
Description: Disables all automatic Comet Cache Clear Routines
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('comet_cache_disable_auto_clear_cache_routines', '__comet_cache_disable_auto_clear_cache_routines', 10, 0);

function __comet_cache_disable_auto_clear_cache_routines() {
	return TRUE; // Yes, disable Comet Cache Clear Routines
}

```

## Disabling 'Wipe Cache' Routines

Inside `wp-content/mu-plugins/` create this file: `zc-disable-auto-wipe-cache-routines.php`:

```php
<?php
/*
Plugin Name: Disable Comet Cache Wipe Cache Routines
Description: Disables all automatic Comet Cache Wipe Cache Routines
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('comet_cache_disable_auto_wipe_cache_routines', '__comet_cache_disable_auto_wipe_cache_routines', 10, 0);

function __comet_cache_disable_auto_wipe_cache_routines() {
	return TRUE; // Yes, disable Comet Cache Wipe Cache Routines
}
```

## Disabling both the 'Clear Cache' and 'Wipe Cache' Routines

Inside `wp-content/mu-plugins/` create this file: `zc-disable-auto-clear-wipe-cache-routines.php`:

```php
<?php
/*
Plugin Name: Disable Comet Cache Clear and Wipe Cache Routines
Description: Disables all automatic Comet Cache Clear and Wipe Cache Routines
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('comet_cache_disable_auto_wipe_cache_routines', '__comet_cache_disable_auto_clear_wipe_cache_routines', 10, 0);
add_filter('comet_cache_disable_auto_clear_cache_routines', '__comet_cache_disable_auto_clear_wipe_cache_routines', 10, 0);

function __comet_cache_disable_auto_clear_wipe_cache_routines() {
	return TRUE; // Yes, disable Comet Cache Clear and Wipe Cache Routines
}
```
