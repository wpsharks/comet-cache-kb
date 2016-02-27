---
title: How to Migrate from ZenCache Pro to Comet Cache Pro
categories: tutorials
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/107
---

When installing the Comet Cache Pro plugin, Comet Cache will automatically detect and preserve any existing ZenCache Pro settings. Once Comet Cache has been activated, ZenCache Pro will be deactivated. All of this happens automatically; all you need to do is install the Comet Cache plugin.

See also: [Announcing Comet Cache™ (formerly ZenCache)](http://cometcache.com/announcing-comet-cache-formerly-zencache/).

## Step-by-Step: Migrating from ZenCache Pro to Comet Cache Pro

As an existing ZenCache Pro customer, your ZenCache Pro license entitles you to a free copy of Comet Cache Pro. There is no need to purchase Comet Cache Pro if you already own ZenCache Pro. Please follow the steps below to use your existing customer account from ZenCache.com to login to CometCache.com, where you'll be able to access Comet Cache Pro and your free Comet Cache Pro license.

1. Collect your existing account details for ZenCache Pro. You will need your username/password for [ZenCache.com](http://zencache.com/); i.e., the old site that was for ZenCache Pro. If you lost those details, you can [recover them here](https://cometcache.com/wp-login.php?action=lostpassword).

2. Use those exact same login credentials to access an account that is _now waiting for you_ at CometCache.com; i.e., please [log into CometCache.com](https://cometcache.com/wp-login.php) with your existing ZenCache.com username/password. _This works for existing ZenCache Pro customers only._

     ![2016-02-19_15-40-34](https://cloud.githubusercontent.com/assets/53005/13188524/f9e2f1b2-d71f-11e5-9f22-f92c062baf41.png)


3. Visit your [My Account page at CometCache.com](http://cometcache.com/account/), where you may now obtain a free copy of Comet Cache Pro. Please download the `comet-cache-pro.zip` file from this page.

     ![2016-02-19_15-44-39](https://cloud.githubusercontent.com/assets/53005/13188483/c8a17aec-d71f-11e5-8376-ff8fd35d5b7d.png)

4. If you have ZenCache or ZenCache Pro currently active, deactivate ZenCache before installing Comet Cache Pro.

     ![2016-02-27_08-42-46](https://cloud.githubusercontent.com/assets/53005/13373181/515b84b8-dd2e-11e5-8bc5-5d760ffcf1d6.png)

5. Now upload and activate `comet-cache-pro.zip` (or it might be named something like: `comet-cache-pro-vXXXXXX.zip`). You can upload the ZIP file using your WordPress Dashboard; i.e. `Dashboard → Plugins → Add New → Upload Plugin`. _See attached screenshots for example._

     ![2015-02-05_05-08-28](https://cloud.githubusercontent.com/assets/1563559/6061535/11454c70-acf5-11e4-8439-2fcd036da63b.png)
     ![2016-02-19_15-49-01](https://cloud.githubusercontent.com/assets/53005/13188633/86f8f196-d720-11e5-9450-2c8bf76331c9.png)
     ![2016-02-19_15-52-03](https://cloud.githubusercontent.com/assets/53005/13188668/c3c4179a-d720-11e5-9a74-37cf70bf5209.png)


## Frequently Asked Questions

### I already paid for ZenCache Pro; do I need to buy Comet Cache Pro?

No. All ZenCache Pro customers receive a free upgrade to Comet Cache Pro.

### How do I install Comet Cache if I already have ZenCache installed?

Please Deactivate ZenCache and/or ZenCache Pro first (_don't_ delete the ZenCache plugin until after you've installed Comet Cache; that way your existing ZenCache options will be preserved in Comet Cache). Then, follow the instructions above to Install and Activate the new Comet Cache Pro plugin. That's it! :-)

### Can I delete ZenCache Pro?

If you have any custom ZenCache settings that you want Comet Cache Pro to import, then you can leave ZenCache installed until after you install Comet Cache. When Comet Cache is installed, it will look for any existing ZenCache plugin settings and copy those over to Comet Cache.

Once Comet Cache has been installed, you can delete the ZenCache plugin.

### Will my old ZenCache settings carry over to Comet Cache?

Yes. If you had ZenCache Pro installed prior to installing Comet Cache Pro, all of your ZenCache Pro configuration options will be picked-up by Comet Cache Pro automatically.

### If I had plugins/themes that were customized to integrate with ZenCache, will those customizations still work with Comet Cache?

Most likely, yes. We have built Comet Cache to be backwards-compatible with ZenCache so if you were using `$GLOBALS['zencache']` or using the `ZENCACHE_ALLOWED` constant, these will still work with Comet Cache.

### What if I don't remember my account details for ZenCache Pro?

See **Step 1** above. You will need your username/password for [ZenCache.com](http://zencache.com/); i.e., the old site that was for ZenCache Pro. If you lost those details, you can [recover them here](https://cometcache.com/wp-login.php?action=lostpassword). You should [log into the new site at CometCache.com](https://cometcache.com/wp-login.php) using the same credentials that you use at ZenCache.com.

If you still have trouble accessing your Comet Cache Pro license, please [open a support ticket](https://cometcache.com/support/) and we'll take care of you.

### If I configure Comet Cache Pro to perform automatic updates, what license key should I enter? The one for ZenCache Pro, or the one for Comet Cache Pro?

Please use a new license key for Comet Cache Pro. You will find your new license key for Comet Cache Pro at CometCache.com. Please check your [My Account](http://cometcache.com/account/) page.

### I received a Fatal Error while migrating; help!

If the error is preventing you from accessing your WordPress Admin Dashboard, start over from scratch by following these [manual uninstallation instructions](https://cometcache.com/kb-article/how-do-i-uninstall-comet-cache/#toc-86754ab8) for **both** ZenCache and Comet Cache. Once that's done, you can follow the [Comet Cache Pro installation instructions](https://cometcache.com/pro-installation/).

If the fatal error is not preventing you from accessing your WordPress Admin Dashboard, and you're seeing the fatal error while activating Comet Cache or removing ZenCache, see the following section.

#### Fatal Error While Activating Comet Cache or Removing ZenCache

If you can still access your WordPress Dashboard and you're receiving a fatal error message while activating Comet Cache or removing ZenCache, follow these steps:

1. In **WordPress Dashboard → Plugins**, make sure that both ZenCache **and** Comet Cache are deactivated
2. In **WordPress Dashboard → Plugins**, activate ZenCache
3. In **WordPress Dashboard → ZenCache → Plugin Deletion Safeguards**, make sure "Yes, uninstall (completely erase)" is selected and then click "Save All Changes" at the very bottom of the page.
4. In **WordPress Dashboard → Plugins**, deactivate ZenCache
5. In **WordPress Dashboard → Plugins**, delete ZenCache

Now you should be able to activate Comet Cache without issue. If you continue to see a Fatal Error, follow these [manual uninstallation instructions](https://cometcache.com/kb-article/how-do-i-uninstall-comet-cache/#toc-86754ab8) for both ZenCache and Comet Cache, and then try reinstalling Comet Cache.

## Getting Help with Other Issues

If after following all of the steps above, and reading over each of the FAQs, you find yourself with an issue that requires our assistance, please [open a support ticket here](http://cometcache.com/support/); we're happy to help! :-)
