---
title: How to Manually Upgrade ZenCache Pro
categories: tutorials
tags: installation-upgrade
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/45
---

In most cases, you can follow the [ZenCache Pro Installation](https://zencache.com/pro-installation/) instructions the first time and then configure the Pro Plugin Updater (**WordPress Dashboard → ZenCache → Plugin Updater**) to keep ZenCache Pro updated. However, some web hosts block the Pro Plugin Updater from working correctly, resulting in [a 404 error](https://zencache.com/kb-article/why-am-i-getting-a-404-error-when-running-the-pro-updater/). 

If you cannot get your web host to work correctly with the Pro Plugin Updater, or if you have some other scenario that requires you to manually update ZenCache, then you can follow the instructions below to manually upgrade ZenCache Pro whenever an update is available.

1. [Log into ZenCache.com](https://zencache.com/wp-login.php) to download the latest version of ZenCache Pro.

     ![2015-02-04_18-20-37](https://cloud.githubusercontent.com/assets/1563559/6054499/92df2702-ac9a-11e4-8b91-c1a85a1f4d5c.png)

2. Visit your [My Account page at ZenCache.com](http://zencache.com/account/), where you may now obtain the latest version of ZenCache Pro. Please download the `zencache-pro.zip` file from this page.

     ![2015-02-05_05-04-05](https://cloud.githubusercontent.com/assets/1563559/6061450/795993b2-acf4-11e4-802e-5d969a651662.png)

3. Now before manually upgrading ZenCache Pro, we should make sure that your existing ZenCache options remain preserved. Visit **WordPress Dashboard → ZenCache → Plugin Options → Plugin Deletion Safeguards** and make sure that "Safeguard my options and the cache" is selected.

     ![2015-03-19_12-54-37](https://cloud.githubusercontent.com/assets/53005/6736074/0102d11a-ce39-11e4-8536-a50b880455db.png)
     ![2015-03-19_12-56-06](https://cloud.githubusercontent.com/assets/53005/6736083/07335348-ce39-11e4-8de2-1fb4d537e55d.png)

4. Now we need to **Deactivate** and then **Delete** the old ZenCache Pro plugin so that we can install the new version.

     ![2015-03-19_12-57-44](https://cloud.githubusercontent.com/assets/53005/6736111/346f5960-ce39-11e4-9269-b6361d54fba9.png)
     ![2015-03-19_12-58-22](https://cloud.githubusercontent.com/assets/53005/6736114/361e6800-ce39-11e4-8916-2b569e3651c5.png)
     ![2015-03-19_12-58-41](https://cloud.githubusercontent.com/assets/53005/6736115/37f41134-ce39-11e4-904f-4b5d9b25b01b.png)

5. Once the old version has been deleted, visit **WordPress Dashboard → Plugins → Add New** to upload and install the new version of ZenCache Pro.

     ![2015-03-19_12-59-16](https://cloud.githubusercontent.com/assets/53005/6736137/58e42e38-ce39-11e4-9601-46567c76b03d.png)

6. Now upload and activate the `zencache-pro.zip` (or it might be named something like: `zencache-pro-vXXXXXX.zip`) file that you downloaded from ZenCache.com. You can upload the ZIP file using your WordPress Dashboard; i.e. **Dashboard → Plugins → Add New → Upload Plugin**. _See attached screenshots for example._ 

     ![2015-02-05_05-08-28](https://cloud.githubusercontent.com/assets/1563559/6061535/11454c70-acf5-11e4-8439-2fcd036da63b.png)
     ![2015-02-05_05-15-30](https://cloud.githubusercontent.com/assets/1563559/6061673/0e38bbb0-acf6-11e4-8cfd-eab2e564583a.png)
     ![2015-02-05_05-16-39](https://cloud.githubusercontent.com/assets/1563559/6061701/39386180-acf6-11e4-904a-57ae77088b55.png)

7. Once ZenCache Pro has been activated, you can confirm that you now have the latest version by looking at the version number and comparing that to the latest release at the top of [the changelog](http://zencache.com/changelog/).

     ![2015-03-19_13-06-20](https://cloud.githubusercontent.com/assets/53005/6736261/17e69c76-ce3a-11e4-909b-31449632d72e.png)
