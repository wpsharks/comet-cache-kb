---
title: How do I uninstall Comet Cache?
categories: questions
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/78
toc-enable: on
---

You can completely remove Comet Cache and erase all of the options from the WordPress database by following these steps:

1. Disable Plugin Deletion Safeguards in **WordPress Dashboard → Comet Cache → Plugin Options → Plugin Deletion Safeguards**
1. Locate the Comet Cache plugin in **WordPress Dashboard → Plugins** and choose "Deactivate"
1. Locate the Comet Cache plugin in **WordPress Dashboard → Plugins** and choose "Delete"
1. Click "Yes, Delete these files and data"

The Comet Cache plugin and all its files and data will then be completely removed from your WordPress site.

## What if I want to keep my custom settings?

To delete Comet Cache but retain your custom settings, simply follow the steps above, but skip step 1.

If you leave "Plugin Deletion Safeguards" enabled, deleting the Comet Cache the plugin does not erase any of the settings from the WordPress database and when you reinstall Comet Cache, those existing options in the database will be used and your previous configuration will be restored.

If you're using Comet Cache Pro, you can export your Comet Cache options from **WordPress Dashboard → Comet Cache → Plugin Options → Import/Export Options** and then reimport those options later (either after reinstalling Comet Cache or even on another WordPress site).

## How do I manually uninstall via FTP?

To uninstall Comet Cache or Comet Cache Pro via FTP, follow these steps:

1. Edit your `wp-config.php` file and remove the line at the top that says `define(WP_CACHE, TRUE);`
1. Delete the `advanced-cache.php` file from inside `wp-content`
1. Delete the `comet-cache` or `comet-cache-pro` directory from inside `wp-content/plugins/`
1. Delete the `comet-cache` directory from inside `wp-content/cache/`

The Comet Cache plugin has now been removed. Note that removing the plugin manually does not erase any of the plugin options from within the WordPress database. To erase those options, you must disable Plugin Deletion Safeguards and Deactivate/Delete the plugin from the WordPress Dashboard.

### How do I manually uninstall ZenCache?

The instructions for manually uninstalling ZenCache are the same as for Comet Cache. Simply replace `comet-cache` or `comet-cache-pro` with `zencache` or `zencache-pro`. 
