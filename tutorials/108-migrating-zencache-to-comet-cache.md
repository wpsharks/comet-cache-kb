---
title: How to Migrate from ZenCache (Lite) to Comet Cache (Lite)
categories: tutorials
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/108
toc-enable: true
---

When installing the Comet Cache plugin, Comet Cache will automatically detect and preserve any existing ZenCache settings. Once Comet Cache has been activated, ZenCache will be deactivated. All of this happens automatically; all you need to do is install the Comet Cache plugin.

See also: [Announcing Comet Cache™ (formerly ZenCache)](http://cometcache.com/announcing-comet-cache-formerly-zencache/).

## Step-by-Step: Migrating from ZenCache to Comet Cache

There are two ways to install Comet Cache:

### Installing Comet Cache via the WordPress Dashboard

1. Log in to your WordPress Dashboard and go to `Dashboard → Plugins → Add New` in the sidebar and then search the Plugin Repository for "Comet Cache".
1. Click the "Install Now" button for the Comet Cache plugin; it should be at the top of the search results.
1. Click the "Activate Now" link when Comet Cache finishes downloading
1. (Optional Step) Now that you've deactivated the ZenCache plugin, you can also Delete it, as there is no need to have both ZenCache and Comet Cache installed.

### Installing Comet Cache via Downloaded Zip File

1. Download the Comet Cache plugin from [WordPress.org](https://wordpress.org/plugins/comet-cache/) or from [cometcache.com](https://cometcache.com/account/)
1. Log in to your WordPress Dashboard and Visit `Dashboard → Plugins → Add New`
1. Click the `Upload Plugin` button
1. (Optional Step) Now that you've deactivated the ZenCache plugin, you can also Delete it, as there is no need to have both ZenCache and Comet Cache installed.

That's it! If you had ZenCache installed prior to installing Comet Cache, you should see a migration message like the one below:

![2016-02-19_14-34-06](https://cloud.githubusercontent.com/assets/53005/13186801/d8dcc72c-d715-11e5-987e-4936658d734f.png)

You'll also now see a new "Comet Cache" icon in the WordPress Dashboard Sidebar:

![2016-02-19_15-13-23](https://cloud.githubusercontent.com/assets/53005/13187775/64c1fce4-d71b-11e5-9dcb-aa291a4ebbba.png)

## Frequently Asked Questions

### I already have ZenCache installed; how do I install Comet Cache?

You can simply install Comet Cache. The Comet Cache installation routine will automatically detect ZenCache, migrate over your ZenCache settings, and then deactivate the ZenCache plugin. Please see the full tutorial above under _How to Migrate from ZenCache to Comet Cache_.

### Will my old ZenCache settings carry over to Comet Cache?

Yes. If you had ZenCache installed prior to installing Comet Cache, all of your ZenCache configuration options will be picked-up by Comet Cache automatically.

### Can I delete ZenCache before installing Comet Cache?

If you don't have any custom ZenCache settings that you want Comet Cache to import, then yes you can delete ZenCache before installing Comet Cache. ZenCache _is not_ required to install Comet Cache.

### If I had plugins/themes that were customized to integrate with ZenCache, will those customizations still work with Comet Cache?

Most likely, yes. We have built Comet Cache to be backwards-compatible with ZenCache so if you were using `$GLOBALS['zencache']` or using the `ZENCACHE_ALLOWED` constant, these will still work with Comet Cache.

### How do I install Comet Cache if I already have ZenCache installed?

When installing the Comet Cache plugin, Comet Cache will automatically detect and preserve your existing ZenCache settings. Once Comet Cache has been activated, ZenCache will be deactivated. All of this happens automatically; all you need to do is install the Comet Cache plugin. That's it! :-)

## Getting Help with Other Issues

If after following all of the steps above, and reading over each of the FAQs, you find yourself with an issue that requires assistance, please start a new thread on the [Comet Cache Community Forum](https://cometcache.com/r/community-forum/).
