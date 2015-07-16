---
title: How do I know if ZenCache is working?
categories: questions
tags: enabledisable
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/48
toc-enable: on
---

ZenCache will add "HTML Notes" to the bottom of every page when it ZenCache enabled and you have the HTML Notes option enabled (enabled by default). To verify that ZenCache is enabled and the HTML Notes option is turned on, visit **ZenCache → Plugin Options → Enable/Disable**:

![2015-03-21_20-51-57](https://cloud.githubusercontent.com/assets/53005/6767556/b5b0c124-d00c-11e4-8ca4-ba13a16295f3.png)

Once you have verified that ZenCache is enabled and the HTML Notes option is turned on, you can logout of WordPress (caching is disabled for logged-in users by default, so you'll need to logout) and then visit the home page of your site and choose the "View Source" option in your browser:

<div class="li-margins"></div>
- Internet Explorer: **View → Source**
- Google Chrome: **View → Developer → View Source**
- Mozilla Firefox: **Tools → Web Developer → Page Source**
- Apple Safari: Visit **Safari → Preferences → Advanced** and enable "Show Developer menu in menu bar". Then you can visit **Developer → Show Page Source**

You'll want to scroll all the way to the bottom of the source and look for the HTML Notes added by ZenCache. They should look something like this:

![2015-03-21_20-47-55](https://cloud.githubusercontent.com/assets/53005/6767563/f80d40ce-d00c-11e4-8891-0f110a005d97.png)

If you see "ZenCache fully functional", then you know ZenCache is enabled and working properly.

## What if I just see blank lines at the bottom?

If you don't see any HTML Notes added by ZenCache but you do see several empty lines where you'd expect to the see the notes, then you could have another plugin or another service stripping out HTML Notes from your site. CloudFlare is known to do this when the "Minify" option is enabled, for example.

![2015-03-21_20-49-43](https://cloud.githubusercontent.com/assets/53005/6767568/3787d2aa-d00d-11e4-9e73-4f026181b44b.png)

This does not mean that ZenCache isn't working. It just means that the HTML Notes that ZenCache adds for informational purposes are being stripped out. If you want to verify that ZenCache is actually working, you can temporarily disable any other "HTML Compression" or "Minify" options that you're running.

_**Note:** If you're using ZenCache Pro with the HTML Compression option, ZenCache will not strip out its own HTML Notes._

## ZenCache is enabled but not working!

If ZenCache is enabled but does not appear to be working, here are a few things you can check:

- Try clicking the "Restore" button inside the ZenCache options to reset the ZenCache configuration. Note that this restores all of the default options, so if you have customized your ZenCache configuration you should back it up before doing this (if you have ZenCache Pro, you can backup your options in **ZenCache → Plugin Options → Import/Export Options**). 
- Make sure there are no other WordPress caching plugins enabled. Only one WordPress caching plugin can be running at a time.
- Check your `.htaccess` file for code that may have bene added by other caching plugins. Some caching plugins, such as WP Super Cache and W3TC do not "clean up" after themselves when uninstalled and will leave behind code inside the `.htaccess` file that can cause issues if you try using another caching plugin.
- The `wp-config.php` file should have a line at the top that says `define(WP_CACHE, TRUE);`--there should be no other lines that mention `WP_CACHE` inside the `wp-config.php` file, only that one line at the top, right below `<?php`. This is what _enables_ caching on a WordPress site. If `WP_CACHE` is set to true, then WordPress will load the caching system defined inside the `wp-content/advanced-cache.php` file (see next point). 
- The `wp-content/advanced-cache.php` file should contain PHP code that mentions ZenCache at the top of the file. This is the file that all WordPress caching plugins use to "hook into" WordPress, so if you installed another caching plugin on your site the `advanced-cache.php` file may be missing, corrupt, or contain code from another caching plugin. ZenCache tries to ensure this cache file exists and contains the right content, but in some scenarios it may be necessary to deactivate ZenCache, delete the `advanced-cache.php` file, and then reactivate ZenCache so that it can reinstall the file with the correct code inside.
