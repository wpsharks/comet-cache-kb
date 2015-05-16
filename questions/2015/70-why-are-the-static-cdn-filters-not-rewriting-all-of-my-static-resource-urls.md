---
title: Why are the Static CDN Filters not rewriting all of my static resource URLs?
categories: questions
tags: static-cdn-filters
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/70
toc-enable: off
---

When the ZenCache Static CDN Filters are enabled, ZenCache will attempt to rewrite all static resource URLs on your site so that those resources point to the configured CDN. If some of your static resource URLs are not changing and you've verified that those file extensions and URIs have not been excluded via the **Blacklisted File Extensions** or **Blacklisted URI Exclusion Patterns** (see **WordPress Dashboard → ZenCache → Plugin Options → Static CDN Filters**), then your WordPress theme, and/or one or more of your WordPress plugins, may not be implementing proper WordPress coding standards, thereby preventing ZenCache from properly rewriting those URLs.

The [WordPress Plugin API](https://codex.wordpress.org/Plugin_API) provides many hooks that allow other WordPress plugins, such as ZenCache, to "filter" the values of things (such as URLs) so that they can be changed in a dynamic way. However, if a WordPress theme or plugin does not implement the Plugin API, then other plugins (such as ZenCache) won't be able to change any of that content (e.g., a URL).

## A Common Mistake: `WP_CONTENT_URL`

An example of a common mistake that we've seen other WordPress plugin and theme developers make is referencing `WP_CONTENT_URL` directly in their theme or plugin, instead of properly calling `content_url()` (see [WordPress Codex](http://codex.wordpress.org/Function_Reference/content_url)). 

If a developer uses `WP_CONTENT_URL` instead of `content_url()`, then ZenCache has no way of rewriting the URLs to static resources referenced by the theme or plugin. As a result, when you enable Static CDN Filters and view your site source code, you may see that only some of the static resources are pointing at your CDN.

## Important Functions for WordPress Plugin/Theme Developers

Here are the most common functions used when constructing links to static resources in a WordPress plugin or theme:

- `site_url()` (see [Function_Reference/site_url](http://codex.wordpress.org/Function_Reference/site_url))
- `content_url()` (see [WordPress Function_Reference/content_url](http://codex.wordpress.org/Function_Reference/content_url))
- `plugins_url()` (see [WordPress Function_Reference/plugins_url](http://codex.wordpress.org/Function_Reference/plugins_url))
- `wp_enqueue_script()` (see [WordPress Function_Reference/wp_enqueue_script](http://codex.wordpress.org/Function_Reference/wp_enqueue_script)
- `wp_enqueue_style()` (see [WordPress Function_Reference/wp_enqueue_style](http://codex.wordpress.org/Function_Reference/wp_enqueue_style))

If a theme or plugin developer follows best-practice and uses these functions when building links to static resources, the ZenCache Static CDN Filters won't have any problem rewriting the URLs to use the CDN.

## How can I fix my theme or plugin?

If you are experiencing an issue with the ZenCache Static CDN Filters not rewriting all URLs to your static resources, we suggest contacting your theme/plugin developer to inform them of this issue with their theme/plugin. You can reference this KB Article when contacting them.
