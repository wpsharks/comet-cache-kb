---
title: How do I uninstall ZenCache?
categories: questions
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/78
toc-enable: off
---

You can completely remove ZenCache and erase all of the options from the WordPress database by following these steps:

1. Disable Plugin Deletion Safeguards in **WordPress Dashboard → ZenCache → Plugin Options → Plugin Deletion Safeguards**
1. Locate the ZenCache plugin in **WordPress Dashboard → Plugins** and choose "Deactivate"
1. Locate the ZenCache plugin in **WordPress Dashboard → Plugins** and choose "Delete" 
1. Click "Yes, Delete these files and data"

The ZenCache plugin and all its files and data will then be completely removed from your WordPress site.

## What if I want to keep my custom settings?

To delete ZenCache but retain your custom settings, simply follow the steps above, but skip step 1. 

If you leave "Plugin Deletion Safeguards" enabled, deleting the ZenCache the plugin does not erase any of the settings from the WordPress database and when you reinstall ZenCache, those existing options in the database will be used and your previous configuration will be restored.

If you're using ZenCache Pro, you can export your ZenCache options from **WordPress Dashboard → ZenCache → Plugin Options → Import/Export Options** and then reimport those options later (either after reinstalling ZenCache or even on another WordPress site). 

## How do I manually uninstall via FTP?

To uninstall ZenCache or ZenCache Pro via FTP, follow these steps:

1. Edit your `wp-config.php` file and remove the line at the top that says `define(WP_CACHE, TRUE);`
1. Delete the `advanced-cache.php` file from inside `wp-content`
1. Delete the `zencache` or `zencache-pro` directory from inside `wp-content/plugins/`

The ZenCache plugin has now been removed. Note that removing the plugin manually does not erase any of the plugin options inside the WordPress database. To erase those options, you must disable Plugin Deletion Safeguards and Deactivate/Delete the plugin from the WordPress Dashboard.
