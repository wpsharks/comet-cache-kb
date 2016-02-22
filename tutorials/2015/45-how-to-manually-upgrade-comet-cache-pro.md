---
title: How to Manually Upgrade Comet Cache Pro
categories: tutorials
tags: installation-upgrade
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/45
toc-enable: off
---

In most cases, you can follow the [Comet Cache Pro Installation](https://cometcache.com/pro-installation/) instructions the first time and then configure the Pro Plugin Updater (**WordPress Dashboard → Comet Cache → Plugin Updater**) to keep Comet Cache Pro updated. However, some web hosts block the Pro Plugin Updater from working correctly, resulting in [a 404 error](https://cometcache.com/kb-article/why-am-i-getting-a-404-error-when-running-the-pro-updater/).

If you cannot get your web host to work correctly with the Pro Plugin Updater, or if you have some other scenario that requires you to manually update Comet Cache, then you can follow the instructions below to manually upgrade Comet Cache Pro whenever an update is available.

## Step-by-Step: Upgrading Comet Cache Pro Manually

1. [Log into cometcache.com](https://cometcache.com/wp-login.php) to download the latest version of Comet Cache Pro.

     ![CometCache.com Login](https://cloud.githubusercontent.com/assets/53005/13232779/a256bcce-d97e-11e5-952f-59f1f52718ca.png)

2. Visit your [My Account page at cometcache.com](http://cometcache.com/account/), where you may now obtain the latest version of Comet Cache Pro. Please download the `comet-cache-pro.zip` file from this page.

     ![CometCache.com My Account](https://cloud.githubusercontent.com/assets/53005/13232819/c8615708-d97e-11e5-8f0f-dcedab7a44da.png)

3. Now before manually upgrading Comet Cache Pro, we should make sure that your existing Comet Cache options remain preserved. Visit **WordPress Dashboard → Comet Cache → Plugin Options → Plugin Deletion Safeguards** and make sure that "Safeguard my options and the cache" is selected.

     ![2016-02-22_16-12-59](https://cloud.githubusercontent.com/assets/53005/13233337/49d0d532-d981-11e5-98b8-0020e3e622de.png)
     ![2016-02-22_16-13-45](https://cloud.githubusercontent.com/assets/53005/13233344/4c40a3b0-d981-11e5-9f58-251734029940.png)

4. Now we need to **Deactivate** and then **Delete** the old Comet Cache Pro plugin so that we can install the new version. As long as the Plugin Deletion Safeguards are enabled (see previous step), you will not lose any of your existing Comet Cache Options in this step.

     ![2016-02-22_16-15-24](https://cloud.githubusercontent.com/assets/53005/13233364/67bdeb70-d981-11e5-8cdb-7bdf31da8036.png)
     ![2016-02-22_16-17-06](https://cloud.githubusercontent.com/assets/53005/13233370/6ab8e460-d981-11e5-8870-54daf99fdeb3.png)
     ![2016-02-22_16-16-04](https://cloud.githubusercontent.com/assets/53005/13233380/741ea5ee-d981-11e5-9ed1-7c27f2a1faf6.png)

5. Once the old version has been deleted, you can upload and activate the latest version of Comet Cache Pro, which you downloaded earlier. Visit **WordPress Dashboard → Plugins → Add New** to upload and install the new version of Comet Cache Pro.

     ![2016-02-22_16-17-45](https://cloud.githubusercontent.com/assets/53005/13233406/8ccd87d6-d981-11e5-8041-79759f6281dc.png)

6. Now upload and activate the `comet-cache-pro.zip` (or it might be named something like: `comet-cache-pro-vXXXXXX.zip`) file that you downloaded from cometcache.com. You can upload the ZIP file using your WordPress Dashboard; i.e. **Dashboard → Plugins → Add New → Upload Plugin**. _See attached screenshots for example._

     ![2016-02-22_16-18-30](https://cloud.githubusercontent.com/assets/53005/13233422/9c99b81a-d981-11e5-95c2-59a076bfe042.png)
     ![2016-02-22_16-19-04](https://cloud.githubusercontent.com/assets/53005/13233423/9d31ebf8-d981-11e5-86ad-d4ff83895171.png)
     ![2016-02-22_16-19-18](https://cloud.githubusercontent.com/assets/53005/13233426/9f124530-d981-11e5-95cb-e0b389ae058b.png)

7. Once Comet Cache Pro has been activated, you can confirm that you now have the latest version by looking at the version number and comparing that to the latest release at the top of [the changelog](http://cometcache.com/changelog/).

     ![2016-02-22_16-20-13](https://cloud.githubusercontent.com/assets/53005/13233452/b1923d82-d981-11e5-98fb-f29e9d36a47c.png)
