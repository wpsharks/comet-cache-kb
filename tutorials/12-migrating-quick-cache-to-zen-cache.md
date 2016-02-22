---
title: How to Migrate from Quick Cache (Lite) to Comet Cache (Lite)
categories: tutorials
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/12
toc-enable: true
---

https://www.youtube.com/watch?v=gmuU2zC1UIE

## Step-by-Step: Migrating from Quick Cache to Comet Cache

See also: [Announcing Comet Cache™ (formerly Quick Cache)](http://cometcache.com/announcing-comet-cache-formerly-quick-cache/).

When installing the Comet Cache plugin, Comet Cache will automatically detect and preserve your existing Quick Cache settings. Once Comet Cache has been activated, Quick Cache will be deactivated. All of this happens automatically; all you need to do is install the Comet Cache plugin.

There are two ways to install Comet Cache:

### Installing Comet Cache via the WordPress Dashboard

1. Log in to your WordPress Dashboard and go to `Plugins ⥱ Add New` in the sidebar and then search the Plugin Repository for "Comet Cache".
1. Click the "Install Now" button for the Comet Cache plugin; it should be at the top of the search results.
1. Click the "Activate Now" link when Comet Cache finishes downloading
1. (Optional Step) Now that you've deactivated the Quick Cache plugin, you can also Delete it, as there is no need to have both Quick Cache and Comet Cache installed.

### Installing Comet Cache via Downloaded Zip File

1. Download the Comet Cache plugin from [WordPress.org](https://wordpress.org/plugins/comet-cache/) or from [cometcache.com](https://cometcache.com/account/)
1. Log in to your WordPress Dashboard and Visit `Plugins ⥱ Add New`
1. Click the `Upload Plugin` button
1. (Optional Step) Now that you've deactivated the Quick Cache plugin, you can also Delete it, as there is no need to have both Quick Cache and Comet Cache installed.

That's it! If you had Quick Cache installed prior to installing Comet Cache, you should see a migration message like the one below:

![2015-02-10_21-40-18](https://cloud.githubusercontent.com/assets/53005/6141023/97ef3548-b16d-11e4-9151-cda7c37c6ca1.png)


You'll also now see a new "Comet Cache" icon in the WordPress Dashboard Sidebar:

![2015-02-04_22-54-46](https://cloud.githubusercontent.com/assets/53005/6054828/dabc9610-acc0-11e4-8dd9-642c7e51a688.png)

## Frequently Asked Questions

### I already have Quick Cache installed; how do I install Comet Cache?

You will need to disable Quick Cache and then install Comet Cache. We recommend also clearing your Quick Cache cache and then deleting the plugin before installing Comet Cache. Please see the full tutorial above under _How to Migrate from Quick Cache to Comet Cache_.

### Can I delete Quick Cache before installing Comet Cache?

If you don't have any custom Quick Cache settings that you want Comet Cache to import, then yes you can delete Quick Cache before installing Comet Cache. Quick Cache _is not_ required to install Comet Cache.

### Will my old Quick Cache settings carry over to Comet Cache?

Yes. If you had Quick Cache installed prior to installing Comet Cache, all of your Quick Cache configuration options will be picked-up by Comet Cache automatically.

### If I had plugins/themes that were customized to integrate with Quick Cache, will those customizations still work with Comet Cache?

Most likely, yes. We have built Comet Cache to be backwards-compatible with Quick Cache so if you were using `$GLOBALS['quick_cache']` or using the `QUICK_CACHE_ALLOWED` constant, these will still work with Comet Cache.

### How do I install Comet Cache if I already have Quick Cache installed?

When installing the Comet Cache plugin, Comet Cache will automatically detect and preserve your existing Quick Cache settings. Once Comet Cache has been activated, Quick Cache will be deactivated. All of this happens automatically; all you need to do is install the Comet Cache plugin. That's it! :-)

## Getting Help with Other Issues

If after following all of the steps above, and reading over each of the FAQs, you find yourself with an issue that requires assistance, please start a new thread on the [Comet Cache Community Forum](http://wordpress.org/support/plugin/comet-cache).
