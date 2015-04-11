---
title: How do I install or update ZenCache via FTP/SFTP?
categories: questions
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/60
toc-enable: off
---

If you cannot [install or upgrade ZenCache Pro via the WordPress Dashboard](http://zencache.com/kb-article/how-to-manually-upgrade-zencache-pro/), perhaps because your web hosting company is blocking the requests to WebSharks' servers (see [Why am I getting a 404 error?](https://zencache.com/kb-article/why-am-i-getting-a-404-error-when-running-the-pro-updater/)), then you may need to use FTP/SFTP to install or upgrade ZenCache Pro.

1. If you are upgrading ZenCache, visit **WordPress Dashboard → ZenCache → Plugin Options → Plugin Deletion Safeguards** first and make sure that "Safeguard my options" is selected; this will ensure that you don't lose any of your existing ZenCache configuration when upgrading.
1. Deactivate and delete ZenCache, if it is currently installed.
1. Download the `zencache-pro.zip` file from [your account](/account/) at ZenCache.com.
1. Unzip the file you downloaded; you should now have a folder called `zencache-pro`.
1. Login to your site via FTP/SFTP and navigate to `wp-content/plugins/`
1. If there is an existing `zencache-pro` folder inside `wp-content/plugins/`, delete it (or you can overwrite it with the new folder).
1. Upload the new `zencache-pro` folder (the one you unzipped) to `wp-content/plugins/`
1. When finished uploading, visit **WordPress Dashboard → Plugins**, locate ZenCache Pro in the list of installed plugins, and click **Activate** on ZenCache Pro.
1. Once the plugin is active, you can go to **WordPress Dashboard → ZenCache → Plugin Options → Enable/Disable**, and Enable ZenCache.

That's it! The latest version of ZenCache Pro has now been installed or upgraded.
