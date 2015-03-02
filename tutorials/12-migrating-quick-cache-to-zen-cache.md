---
title: How to Migrate from Quick Cache (Lite) to ZenCache (Lite)
categories: tutorials
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/12
toc-enable: true
---

https://www.youtube.com/watch?v=gmuU2zC1UIE

## Step-by-Step: Migrating from Quick Cache to ZenCache

See also: [Announcing ZenCache™ (formerly Quick Cache)](http://zencache.com/announcing-zencache-formerly-quick-cache/).

When installing the ZenCache plugin, ZenCache will automatically detect and preserve your existing Quick Cache settings. Once ZenCache has been activated, Quick Cache will be deactivated. All of this happens automatically; all you need to do is install the ZenCache plugin.

There are two ways to install ZenCache:

### Installing ZenCache via the WordPress Dashboard

1. Log in to your WordPress Dashboard and go to `Plugins ⥱ Add New` in the sidebar and then search the Plugin Repository for "ZenCache".
1. Click the "Install Now" button for the ZenCache plugin; it should be at the top of the search results.
1. Click the "Activate Now" link when ZenCache finishes downloading
1. (Optional Step) Now that you've deactivated the Quick Cache plugin, you can also Delete it, as there is no need to have both Quick Cache and ZenCache installed.

### Installing ZenCache via Downloaded Zip File

1. Download the ZenCache plugin from [WordPress.org](https://wordpress.org/plugins/zencache/) or from [ZenCache.com](https://zencache.com/account/)
1. Log in to your WordPress Dashboard and Visit `Plugins ⥱ Add New`
1. Click the `Upload Plugin` button
1. (Optional Step) Now that you've deactivated the Quick Cache plugin, you can also Delete it, as there is no need to have both Quick Cache and ZenCache installed.

That's it! If you had Quick Cache installed prior to installing ZenCache, you should see a migration message like the one below:

![2015-02-10_21-40-18](https://cloud.githubusercontent.com/assets/53005/6141023/97ef3548-b16d-11e4-9151-cda7c37c6ca1.png)


You'll also now see a new "ZenCache" icon in the WordPress Dashboard Sidebar:

![2015-02-04_22-54-46](https://cloud.githubusercontent.com/assets/53005/6054828/dabc9610-acc0-11e4-8dd9-642c7e51a688.png)
 
## Frequently Asked Questions

### I already have Quick Cache installed; how do I install ZenCache?

You will need to disable Quick Cache and then install ZenCache. We recommend also clearing your Quick Cache cache and then deleting the plugin before installing ZenCache. Please see the full tutorial above under _How to Migrate from Quick Cache to ZenCache_.

### Can I delete Quick Cache before installing ZenCache?

If you don't have any custom Quick Cache settings that you want ZenCache to import, then yes you can delete Quick Cache before installing ZenCache. Quick Cache _is not_ required to install ZenCache.

### Will my old Quick Cache settings carry over to ZenCache?

Yes. If you had Quick Cache installed prior to installing ZenCache, all of your Quick Cache configuration options will be picked-up by ZenCache automatically.

### How do I install ZenCache if I already have Quick Cache installed?

When installing the ZenCache plugin, ZenCache will automatically detect and preserve your existing Quick Cache settings. Once ZenCache has been activated, Quick Cache will be deactivated. All of this happens automatically; all you need to do is install the ZenCache plugin. That's it! :-)

## Getting Help with Other Issues

If after following all of the steps above, and reading over each of the FAQs, you find yourself with an issue that requires assistance, please start a new thread on the [ZenCache Community Forum](http://wordpress.org/support/plugin/zencache).
