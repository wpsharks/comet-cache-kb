---
title: How do I install or update Comet Cache via FTP/SFTP?
categories: questions
tags: installation-upgrading
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/60
toc-enable: off
---

If you cannot [install or upgrade Comet Cache Pro via the WordPress Dashboard](http://cometcache.com/kb-article/how-to-manually-upgrade-comet-cache-pro/) (perhaps because your web hosting company is blocking the requests to WebSharks' servers; see [Why am I getting a 404 error?](https://cometcache.com/kb-article/why-am-i-getting-a-404-error-when-running-the-pro-updater/)), then you may need to use FTP/SFTP to install or upgrade Comet Cache Pro.

Follow these steps to install or upgrade Comet Cache Pro via FTP or SFTP:

1. If you are upgrading Comet Cache, visit **WordPress Dashboard → Comet Cache → Plugin Options → Plugin Deletion Safeguards** first and make sure that "Safeguard my options" is selected; this will ensure that you don't lose any of your existing Comet Cache configuration when upgrading.
1. Deactivate and delete Comet Cache, if it is currently installed.
1. Download the `comet-cache-pro.zip` file from [your account](/account/) at cometcache.com.
1. Unzip the file you downloaded; you should now have a folder called `comet-cache-pro`.
1. Login to your site via FTP/SFTP and navigate to `wp-content/plugins/` (if you're not sure how to do this, please contact your web hosting company).
1. If there is an existing `comet-cache-pro` folder inside `wp-content/plugins/`, delete it (or you can overwrite it with the new folder).
1. Upload the new `comet-cache-pro` folder (the one you unzipped) to `wp-content/plugins/`
1. When finished uploading, visit **WordPress Dashboard → Plugins**, locate Comet Cache Pro in the list of installed plugins, and click **Activate** on Comet Cache Pro.
1. Once the plugin is active, you can go to **WordPress Dashboard → Comet Cache → Plugin Options → Enable/Disable**, and Enable Comet Cache.

That's it! The latest version of Comet Cache Pro has now been installed or upgraded.
