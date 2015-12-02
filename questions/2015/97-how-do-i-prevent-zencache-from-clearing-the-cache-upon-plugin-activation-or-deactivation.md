---
title: How do I prevent ZenCache from clearing the cache upon plugin activation or deactivation?
categories: questions
tags: clearing-the-cache, mu-plugins-hacks
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/97
---

ZenCache will automatically clear the cache on your site whenever you activate or deactivate a WordPress plugin. Many WordPress plugins add or change content on your site, so ZenCache clears the cache to ensure that an old cache file is not served to a visitor.

If you are activating and deactivating plugins on a regular basis and want manual control over when the cache is cleared, you can disable this automatic behavior by creating a small [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins).

Create this file and directory: `wp-content/mu-plugins/zc-disable-clear-on-plugin-activate-deactivate.php`:

```php
<?php
/*
Plugin Name: Disable ZenCache Automatic Clear Cache on Plugin Activation/Deactivation
Description: Disables the ZenCache Automatic Clear Cache on Plugin Activation/Deactivation
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('zencache_auto_clear_on_plugin_activation_deactivation', '__zencache_auto_clear_on_plugin_activation_deactivation', 10, 0);

function __zencache_auto_clear_on_plugin_activation_deactivation() {
	return FALSE; // Disable the automatic clear cache on plugin activation/deactivation
}

```