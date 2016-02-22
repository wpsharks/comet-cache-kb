---
title: Why is the entire cache cleared when I modify Categories or Tags?
categories: questions
tags: clearing-the-cache
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/74
toc-enable: off
---

One of Comet Cache's most important tasks is ensuring that an outdated version of the site does not get served to visitors. If you change something on the WordPress Dashboard that affects the front-end of the site, Comet Cache will make sure that it clears the old version of any related cache files so that a new, updated version of the cache can be generated.

Comet Cache clears the cache in the most intelligent way possible, however there are some events that may trigger a clearing of the entire cache. These are considered "significant events" that affect _many_ areas of a site. Some of these include changing WordPress settings, installing a plugin or a theme, and adding, editing, or deleting Categories and Tags.

## What's so special about Categories and Tags? 

Changes to Categories and Tags, which include adding, editing, and deleting actions, nearly always results many small changes to the front-end of the site. That means it's simply not possible for Comet Cache to know exactly which cached pages a Tag or Category name may appear.

For example, let's say that you renamed a tag called `apple` to `banana`. Now think of all the possible places on a website where the tag `apple` might appear: the home page (each post tagged `apple` might have the tag listed underneath it), the post itself (obviously), any Tag archive page that might mention the `apple` tag, any date-based archive pages that might have posts tagged `apple`... the list goes on. If Comet Cache does not clear the entire cache, there may be cached pages on the site that still refer to (now renamed) tag `banana` as `apple`, and therefore Comet Cache would be serving an outdated version of the cache to visitors.

The same is true with Categories. 

There are so many places on the front-end of the site, so many places that may already be cached by Comet Cache, that need to be updated when you make changes to Categories and Tags. That's why the safest thing for Comet Cache to do is to clear the entire cache whenever a Category or Tag is changed in any way (created, modified, or deleted).

## Why is the cache being cleared when I save a new Post as Draft?

Creating a new post and saving it as a Draft does not clear the cache, but creating a new post, _and then creating a new Tag/Category and assigning it to the post_, and then saving the post as a Draft _will_ clear the entire cache (again, creating a new Category / Tag is one of those major events that if we don't clear the cache could result in an outdated version of the site being served to visitors).

## How can I disable the Automatic Clear / Wipe Cache Routines?

If you'd like to disable all of these automatic cache wiping routines and take full manual control of when to wipe the entire cache (using the "Clear Cache" button), they can do that using an MU-Plugin:

- [Disabling Automatic Clear / Wipe Cache Routines](http://cometcache.com/kb-article/disabling-automatic-clear-wipe-cache-routines/)