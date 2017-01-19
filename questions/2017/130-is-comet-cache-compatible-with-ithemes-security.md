---
title: Is Comet Cache compatible with iThemes Security?
categories: questions
tags: themeplugin-developers, troubleshooting
author: renzms
github-issue: https://github.com/websharks/comet-cache-kb/issues/130
---

Yes, Comet Cache is compatible with iThemes Security and other WordPress security plugins that may block access to protect sensitive portions of a WordPress site.

WordPress plugins, such as iThemes Security, may block parts of the WordPress site, including the back-end administration, thus preventing unauthorized visitors from accessing these areas. iThemes Security may also tweak certain features on the Dashboard and/or host file settings for increased security. Comet Cache causes no conflict with iThemes Security in this regard, and enabling most of the recommended settings in the Lite version of iThemes Security has no reported issues with the caching process.

There is no specific set of features needed to configure Comet Cache with iThemes Security.

### What if iThemes Security constantly warns me when Comet Cache caches or clears files?

iThemes Security and other WordPress security plugins may log changes to your site files and notify you of these changes. Comet Cache is a dynamic plugin that quietly caches pages, and depending on your specified configuration(s), it is able to automatically clear, wipe or update the cache on a specified date or upon a triggered event. These changes may alert the security plugin as unsolicited changes. These notifications are a false-positive, and iThemes Security may continue to log these events multiple times.

This can be solved in iThemes Security by adding the cache folder as an exclusion in the `File Change Detection` settings.

>![2017-01-19_20-53-46](https://cloud.githubusercontent.com/assets/13220018/22107756/9a457ce8-de8a-11e6-9488-5b77db28fa39.png)


In the pop-up window, scroll down to the` Files and Folders List` section. Exclude files or folders by clicking the red minus next to the file or folder name. We suggest whitelisting `wp-content/cache/comet-cache/`, or you could whitelist the entire cache directory; i.e., `wp-content/cache`.

>![2017-01-19_21-07-00](https://cloud.githubusercontent.com/assets/13220018/22107874/506866ca-de8b-11e6-97b8-411fcbd07655.png)