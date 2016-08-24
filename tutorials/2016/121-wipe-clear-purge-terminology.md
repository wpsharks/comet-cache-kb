---
title: Wipe Clear Purge Terminology
categories: tutorials
tags: clearing-the-cache
author: renzms
github-issue: https://github.com/websharks/comet-cache-kb/issues/121
---

Comet Cache stores cache files for your site inside the default cache directory located at `wp-content/cache/comet-cache/cache/`. Depending on your configurations, Comet Cache will automatically clear or wipe the cache and will make sure it clears the old cache so an updated version can be generated. This article will explain the differences between the terminology Comet Cache uses in clearing the cache.


## Wipe

- To "**wipe**", is to delete ALL files in the cache directory, for all hosts. This includes, but is not limited to, all systematic `cc-` prefixed files in the main `wp-content/cache/comet-cache/cache/cc-*` directory; and anything else for that matter. A full wipe of the cache can be performed by network admins on a MS network.

  A manual wipe is not necessary (or available) for standard WP installs in the Comet Cache UI. Networks only. That said, a full wipe is automatically performed by Comet Cache on both standard and network installs whenever CC options are changed, when the plugin is reactivated/upgraded; or when the plugin is deactivated and/or uninstalled. In the case of uninstalling, the entire CC base directory is removed also; i.e. `wp-content/cache/comet-cache`.

## Clear

- To "**clear**", is to delete cache files (in whole, or in part), for the current host; _excluding_ systematic `cc-` prefixed files in the main `wp-content/cache/comet-cache/cache/cc-*` directory

   There are two types of "clearing" that CC deals with:

	1. **Manual Clearing** of the entire cache. This will clear all cache-related files (and directories containing them). A manual clearing of the cache will impact the _current host only_. Please note that host specificity is irrelevant on a standard WP install since there is just one host; i.e. a clearing of the cache will simply clear the cache for your site. On a MS network, host specificity _is_ important. The cache will be cleared for the current host only; i.e. whichever child blog's dashboard you are currently logged into whenever you perform a manual clearing of the cache.
	
	2. **Automatic Cache Clearing** deals w/ specific cache files only; i.e. not ALL files, just those that contain specific portions of the site which need to be refreshed for one reason or another. Automatic cache clearing can happen as changes occur on-site or in your dashboard. Comet Cache monitors various components within your WordPress installation, and also provides you with some control over automatic cache clearing behavior (even more control in the Pro version). See: **Dashboard → Comet Cache → Clearing the Cache** for config. options.
	
	  _Note: Automatic cache clearing deals with files only (not directories). This is for speed/optimization. In short, it is not necessary for Comet Cache to remove directories too; it's just the files that really matter. If you would like to clear the entire cache (including directories), please do a manual clearing of the cache, which does remove directories also._

**Multisite Network with Domain Mapping:** When domain mapping is being used on a multisite network, the cache for all domains mapped to the blog is also cleared.

## Purge

- To "**purge**", is to automatically delete any expired cache files for the current host (i.e. old/stale cache files, according to your configured cache expiration time). Purging (aka: garbage collecting) is always automatic; i.e. there is no UI functionality that allows you to purge the cache. 

    Automatic purging routines in Comet Cache are driven by WP Cron, and they are always based on your Cache Expiration Time. See: **Dashboard → Comet Cache → Expiration Time**.

    _Note: It's worth mentioning that Comet Cache will never serve an old/stale cache file, even if automatic purging routines get behind, or have been disabled for some reason (e.g. if your web host does not allow WP Cron). The last modification time for each cache file is always checked (in real-time) before it is served to a visitor. Thus, if a cache file expires (either through an automatic purge, or simply because it is too old), it is automatically regenerated on-the-fly._

_____

_If you'd like to disable all of these automatic cache wiping routines and take full manual control of when to wipe the entire cache,_ please see: [Disabling Automatic Clear / Wipe Cache Routines](https://cometcache.com/kb-article/disabling-automatic-clear-wipe-cache-routines/)

_If you'd like to enable automatic cache wiping routines and have finer control over when to wipe the entire cache,_ please see: [Clearing the Cache Dynamically](https://cometcache.com/kb-article/clearing-the-cache-dynamically/)

Please also see: [What are the Clear Cache and Wipe Cache Routines?](https://cometcache.com/kb-article/what-are-the-clear-cache-and-wipe-cache-routines/)