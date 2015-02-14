---
title: What are the Clear Cache and Wipe Cache Routines?
categories: questions
tags: clearing-the-cache
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/22
---
ZenCache occasionally needs to automatically clear or wipe the cache when certain events on your site occur that may cause the cache files to become outdated. 

For example, if you change your WordPress theme, all of the cache files that were generated when the previous theme was active would contain HTML from the previous theme and would therefore would no longer be current. 

If ZenCache does not automatically clear all of the cache files from the cache directory after you switch your theme, visitors to your site will be served cache files that reflect the previous theme, not the current theme.

## What are Clear Cache Routines?

Clear Cache routines automatically clear all cache files for the current blog. By default, this means everything inside the following directories (assuming the current blog is `http://example.com`):

- `wp-content/cache/zencache/cache/http/example-com/`
- `wp-content/cache/zencache/htmlc/private/http/example-com/`
- `wp-content/cache/zencache/htmlc/public/http/example-com/`

### Events that automatically trigger a clear cache routine

- ZenCache plugin activation 
- Changes to General, Reading, Discussion, or Permalink settings (in **Dashboard → Settings**)
- Changes to the current theme selection (**Dashboard → Appearance → Themes**)
- Change Navigation Menus (**Dashboard → Appearance → Menus**)
- Change Terms (e.g., add/edit/delete Categories, Tags, etc.)
- Change Links (e.g., add/edit/delete Links, if used)
- Upgrade an active WordPress component (e.g., plugins, themes, or WordPress Core updates)

## What are Wipe Cache Routines?

Wipe Cache routines automatically wipe out all cache files in the cache directory. By default, this means everything inside the following directory:

- `wp-content/cache/zencache/`

### Events that automatically trigger a wipe cache routine

- When deleting the ZenCache plugin
- When upgrading to a new version of ZenCache
- When saving (i.e., changing) the ZenCache Options (**Dashboard → ZenCache → Plugin Options**)
- When restoring the default ZenCache Options via the 'Restore' button (**Dashboard → ZenCache → Plugin Options**)

### See also:

- [Disabling Automatic Clear / Wipe Cache Routines](https://zencache.com/kb-article/disabling-automatic-clear-wipe-cache-routines/)
