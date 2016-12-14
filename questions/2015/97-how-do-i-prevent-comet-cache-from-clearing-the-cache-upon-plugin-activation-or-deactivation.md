---
title: How do I prevent Comet Cache from clearing the cache upon plugin activation or deactivation?
categories: questions
tags: clearing-the-cache, mu-plugins-hacks
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/97
---

Comet Cache will automatically clear the cache on your site whenever you activate or deactivate a WordPress plugin. Many WordPress plugins add or change content on your site, so Comet Cache clears the cache to ensure that an old cache file is not served to a visitor.

If you are activating and deactivating plugins on a regular basis and want manual control over when the cache is cleared, you can disable this automatic behavior by creating a small [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins).

Create this file and directory: `wp-content/mu-plugins/zc-disable-clear-on-plugin-activate-deactivate.php`:

```php
<?php
/*
Plugin Name: Disable Comet Cache Automatic Clear Cache on Plugin Activation/Deactivation
Description: Disables the Comet Cache Automatic Clear Cache on Plugin Activation/Deactivation
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('comet_cache_auto_clear_on_plugin_activation_deactivation', '__return_false', 10, 0);
```
