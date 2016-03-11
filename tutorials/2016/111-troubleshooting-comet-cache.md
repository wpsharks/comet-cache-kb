---
title: Troubleshooting Comet Cache
categories: tutorials
tags: enabledisable, troubleshooting, themeplugin-developers, error-messages
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/111
---

If Comet Cache does not appear to be working (see [How do I know if Comet Cache is working?](https://cometcache.com/kb-article/how-do-i-know-if-comet-cache-is-working/)), this article will give you a few suggestions for what to check.

To rule out plugin or theme conflicts, we always recommend [Testing Comet Cache in a Clean WordPress Installation](https://cometcache.com/kb-article/testing-comet-cache-in-a-clean-wordpress-installation/).

## Incompatible Plugins

If you're having issues running Comet Cache, a good first step is to verify that you're not running any of these plugins, which have been known to cause problems:

- **Force Gzip** - Force Gzip uses `ob_gzhandler()`, which Comet Cache is not compatible with. Comet Cache is not compatible with output buffers that attempt to pre-compress HTML output.
- **CSS-JS-Booster** - CSS-JS-Booster uses `ob_gzhandler()`, which Comet Cache is not compatible with. Comet Cache is not compatible with output buffers that attempt to pre-compress HTML output.
- **Mobble** - Mobble provides conditional functions for detecting a variety of mobile devices & tablets. However, since Comet Cache generates caches using PHP Output Buffering, once a cache is generates no PHP functions on that page will be evaluated until the cache is regenerated. If you must use Mobble, you can exclude mobile User-Agents from being cached by Comet Cache (see "Mobile Themes" below).
- **Plainview Activity Monitor** - We have had reports of this plugin possibly causing issues with the cache clearing every time the WordPress Dashboard is accessed. See [this issue](https://github.com/websharks/comet-cache/issues/393#issuecomment-68957833) for more details.
- **Remove WPMU Dashboard Notification Nag** - When this plugin is active, the Comet Cache plugin will fail to activate.
- **Hazel Theme** - The Hazel theme makes very heavy use of JavaScript and CSS and has been known to have issues with the Comet Cache HTML Compressor. 

### Special Note: Minifying and Compressing Plugins

Some plugins strip the HTML Comments from the source of your pages to minify and compress the size of your HTML pages. While these plugins may not conflict with Comet Cache, they would have the side effect of hiding the HTML Notes that added by Comet Cache, which would make it appear as though Comet Cache is not running.

Common culprits are any plugin related to minifying, compressing, or optimizing HTML. Services like CloudFlare also have options for minifying HTML, which strips out the HTML Comments added by Comet Cache (see the CloudFlare section below).

Please try disabling any plugins related to minifying or compressing HTML and see if the Comet Cache HTML notes at the bottom of the source show up.

## Other Caching Plugins

You can only have one WordPress caching plugin enabled at a time. Please make sure that Comet Cache is the only caching plugin active.

If you were using or testing other caching plugins, make sure that your `.htaccess` file does not contain any remnants from those other plugins, as many plugins don't properly clean up after themselves when deactivated. 

Also, all caching plugins are required to use the same `wp-content/advanced-cache.php` file to hook into WordPress for caching. Since all caching plugins use the same file, it's possible another plugin wrote content to that file and is now somehow preventing Comet Cache from updating it. 

You can make sure that Comet Cache is the only plugin using the `advanced-cache.php` file by deactivating all other caching plugins, removing `define('WP_CACHE', TRUE);` from the top of your `wp-config.php` file (if it exists) and then deleting the `wp-content/advanced-cache.php` file. Once you've deleted the file, you can disable and then enable Comet Cache (in **Dashboard → Comet Cache → Plugin Options → Enable/Disable**) to have it rewrite the `advanced-cache.php` file.

As a last-resort, you can try [manually uninstalling Comet Cache](https://cometcache.com/kb-article/how-do-i-uninstall-comet-cache/#toc-86754ab8) and then reinstalling it.

## CloudFlare

Comet Cache is fully compatible with CloudFlare, but if you're using CloudFlare, keep in mind that if you have the **Auto Minify (HTML)** option turned on in CloudFlare, all of the HTML comments will be stripped from your content. The Comet Cache notes that get added to the HTML to tell you that Comet Cache is working properly (see **Dashboard → Comet Cache → Enable/Disable → How Can I Tell Comet Cache is Working?**) are written to the HTML as HTML comments, so CloudFlare will strip those as well.

This might make it seem like Comet Cache isn't running when in fact it is. 

To see if Comet Cache is running properly, you can [temporarily put CloudFlare into Development Mode](https://support.cloudflare.com/hc/en-us/articles/200168246-What-does-CloudFlare-Development-mode-mean-), which disables this Auto Minify functionality and allows you to see the Comet Cache notes in the HTML.

With CloudFlare's "Auto Minify (HTML)" turned on, you might also see 4 blank lines at the very bottom of your source code where you'd expect to find the Comet Cache notes:

![screen shot 2014-03-30 at 7 52 11 pm](https://cloud.githubusercontent.com/assets/53005/2562898/a9c23096-b866-11e3-8615-0125ce9a201e.png)

## Nginx

Comet Cache and Comet Cache Pro both support the Nginx web server. If you're having issues, here are a few things to try:

- If you have Zlib compression enabled, try disabling it.

See also: [Recommended Nginx Configuration for Comet Cache](https://cometcache.com/kb-article/recommended-nginx-configuration-for-comet-cache/)

## Mobile Themes

If you're having issues with your Mobile Theme appearing on the Desktop, or the Desktop Theme appearing on mobile devices, Comet Cache is probably caching your mobile theme and then showing it to all visitors, including your Desktop visitors. To prevent this from happening, you'll need to tell Comet Cache to disable caching for mobile devices. (We're working on a [Mobile Mode](https://github.com/websharks/comet-cache/issues/471) to add full support for mobile caching.)

You can specify a list of User-Agent Exclusion Patterns in **Dashboard → Comet Cache → User-Agent Exclusion Patterns**:

```
iPhone * Mobile
iPod * Mobile
Android * Mobile
BB * Mobile Safari
BlackBerry * Mobile Safari
IEMobile/10.0 * Touch
IEMobile/7.0
IEMobile/9.0
webOS
```

![2016-03-11_07-45-39](https://cloud.githubusercontent.com/assets/53005/13702510/44414e1e-e75d-11e5-9797-c76e26513c0b.png)

## Auto-Cache Engine

When enabled, the Auto-Cache Engine runs every 15 minutes via WP Cron. If the Auto-Cache Engine doesn't seem to be working, you can try manually initiating it by visiting `http://yoursite.com/?comet_cache__auto_cache_cron=yes`.

See also: [Auto-Cache Engine KB Articles](https://cometcache.com/kb/kb-tag/auto-cache-engine/)

## Pro Updater Not Working

See [Why am I getting a 404 or 403 error when running the Pro Updater?](https://cometcache.com/kb-article/why-am-i-getting-a-404-or-403-error-when-running-the-pro-updater/)
