---
title: What are the Clear Cache and Wipe Cache Routines?
categories: questions
tags: clearing-the-cache
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/22
---
Comet Cache occasionally needs to automatically clear or wipe the cache when certain events on your site occur that may cause the cache files to become outdated.

For example, if you change your WordPress theme, all of the cache files that were generated when the previous theme was active would contain HTML from the previous theme and would therefore would no longer be current.

If Comet Cache does not automatically clear all of the cache files from the cache directory after you switch your theme, visitors to your site will be served cache files that reflect the previous theme, not the current theme.

## What are Clear Cache Routines?

Clear Cache routines automatically clear all cache files for the current blog. By default, this means everything inside the following directories (assuming the current blog is `http://example.com`):

- `wp-content/cache/comet-cache/cache/http/example-com/`
- `wp-content/cache/comet-cache/htmlc/private/http/example-com/`
- `wp-content/cache/comet-cache/htmlc/public/http/example-com/`

### Events that automatically trigger a clear cache routine

- Comet Cache plugin activation
- Changes to General, Reading, Discussion, or Permalink settings (in **Dashboard → Settings**)
- Changes to the current theme selection (**Dashboard → Appearance → Themes**)
- Change Navigation Menus (**Dashboard → Appearance → Menus**)
- Change Terms (e.g., add/edit/delete Categories, Tags, etc.)
- Change Links (e.g., add/edit/delete Links, if used)
- Upgrade an active WordPress component (e.g., plugins, themes, or WordPress Core updates)

## What are Wipe Cache Routines?

Wipe Cache routines automatically wipe out all cache files in the cache directory. By default, this means everything inside the following directory:

- `wp-content/cache/comet-cache/`

### Events that automatically trigger a wipe cache routine

- When deleting the Comet Cache plugin
- When upgrading to a new version of Comet Cache
- When saving (i.e., changing) the Comet Cache Options (**Dashboard → Comet Cache → Plugin Options**)
- When restoring the default Comet Cache Options via the 'Restore' button (**Dashboard → Comet Cache → Plugin Options**)

### See also:

- [Disabling Automatic Clear / Wipe Cache Routines](https://cometcache.com/kb-article/disabling-automatic-clear-wipe-cache-routines/)
