---
title: Why isn't my dynamic content updating?
categories: questions
tags: clearing-the-cache
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/34
---

Comet Cache automatically handles updating the cache in many scenarios, such as when you publish a new post, or when you change your WordPress theme. However, some plugins, themes, and widgets do not include support for WordPress caching plugins so the dynamic content they produce doesn't update properly when your site is being cached.

When plugins and themes implement proper WordPress development practices, i.e., by calling the appropriate WordPress actions when they update or change content, then Comet Cache will detect these changes and clear the necessary cache files automatically.

If your a theme or plugin that you installed is not clearing the cache automatically, we recommend contacting the plugin developer and asking if the plugin is compatible with WordPress caching plugins. (You can point them to this page.)

### Why is dynamic content a problem for caching plugins?

WordPress caching plugins use what is called "page caching", which means that they capture the output from WordPress and store that in a static file. When someone visits your site in the future, the page will load very quickly because WordPress doesn't need to generate any of the content--the static cache file is used instead.

This means that anything you have on your site that changes regularly (such as a counter widget, or some other portion that dynamically updates on its own) will no longer be dynamic, as whatever was showing on the site when the cache file was generated is what will be shown the next time someone visits the site.

Comet Cache handles most scenarios where clearing the cache is necessary, such as when you publish or edit a post, or when you change your theme or tweak a WordPress setting. However, some plugins and widgets are not compatible with WordPress caching plugins and they will not update properly when your site is being cached.

## What can I do to fix this?

### Option 1: Exclude the URI(s) that contain dynamic content

If you're using Comet Cache Pro, you can use the **URI Exclusion Patterns** feature (see `Comet Cache → Plugin Options → URI Exclusion Patterns`) to exclude the page that contains the dynamic content so that Comet Cache does not cache that page. (If your dynamic content shows up on all pages, then this technique won't work as it will effectively be the same as disabling caching altogether.)

### Option 2: Clear the cache dynamically with PHP

If the plugin or theme you're using does not include support for WordPress caching plugins, you can write some PHP code that will hook into the plugin and clear the cache whenever a particular event occurs.

You have lots of flexibility here. You can do things like detect which specific post cache needs to be cleared and then tell Comet Cache to only clear the cache file for that particular post. Or you could have Comet Cache clear the entire cache whenever an event occurs.

For a full tutorial, please see [Clearing the Cache Dynamically](http://cometcache.com/kb-article/clearing-the-cache-dynamically/).

### Option 3: Use JavaScript for the dynamic content

The best way to avoid issues with WordPress caching plugins and dynamic content is to have the plugin or theme use JavaScript to update the dynamic portions. If the theme or plugin uses JavaScript to make an AJAX call to the backend to retrieve the latest content, the dynamic portions will work even when the page is cached by WordPress.

JavaScript runs in the client browser and not on the server, so even a cached file will remain dynamic, as the browser will simply request the newest data from the server and the page will be updated to reflect the latest content.

You can ask your theme or plugin developer to use JavaScript to update the dynamic content they generate.

### Option 4: Write an Advanced Cache plugin

Comet Cache includes a powerful Advanced Cache plugin system that allows you to extend Comet Cache by integrating it with other plugins and themes. You can use this functionality to tell Comet Cache to do things like maintain a separate cache file for mobile visitors.

See `Comet Cache ⥱ Plugin Options ⥱ Theme/Plugin Developers` for further details and a link to an example AC Plugin.

## How do other WordPress caching plugins handle this?

Other WordPress caching plugins have experimented with techniques that allow you to prevent a certain portion of a page--such as a specific dynamic portion--to be excluded from the cache, however these implementations are prone to security flaws that can lead to your site being compromised.

We have a feature request open to add "dynamic fragmentation" to Comet Cache (see [GitHub Issue #222](https://github.com/websharks/comet-cache/issues/222)), but we want to make sure that when this feature is implemented it is done so in a way that won't pose security issues. 

If you'd like to see this feature added to Comet Cache, please cast your vote by leaving a comment on the feature request.
