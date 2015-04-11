---
title: Why doesn't ZenCache remove query strings from static resources?
categories: questions
tags: html-compression, static-cdn-filters, get-requests
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/61
---

Many speed testing services such as Google PageSpeed and GTMetrix will reduce your overall score if you don't "Remove Query Strings From Static Resources". What these services don't account for is that WordPress sites _must_ use query strings for static resources.

This dependency on query strings is build right into the WordPress functions used by plugin and theme developers to load JavaScript files ([`wp_enqueue_script`](https://codex.wordpress.org/Function_Reference/wp_enqueue_script) and CSS files ([`wp_enqueue_style`](https://codex.wordpress.org/Function_Reference/wp_enqueue_style)): both include a Version Parameter, which allows the plugin or theme developer to specify the version number of that file. That version number then gets appended to the static resource link as a query string (e.g., `theme-style.css?ver=1.5`).

If a plugin or theme developer chooses _not_ to use this Version Parameter, WordPress will go ahead and add one on its own. See the following from the WordPress Codex regarding the Version Parameter:

> String specifying the script version number, if it has one, which is concatenated to the end of the path as a query string. If no version is specified or set to _false_, then WordPress automatically adds a version number equal to the current version of WordPress you are running. If set to _null_ no version is added. This parameter is used to ensure that the correct version is sent to the client regardless of caching, and so should be included if a version number is available and makes sense for the script.

### Why is a version number necessary?

In a WordPress environment, you will be running many different plugins, each with its own version. You'll also be using a WordPress theme, which also has a specific version and will get updated from time to time.

When someone visits your website, all of the JavaScript and CSS files are _cached_, either in the visitors web browser or, if you're using the [ZenCache Static CDN Filters](http://zencache.com/kb-article/introduction-to-static-cdn-filters/), by your CDN provider.

When you update WordPress, or when you update a WordPress theme or plugin, those cached JavaScript and CSS files will likely change. The only way to tell visitors' browsers and your CDN that the files have changed is to _change the link to the files_. 

How do we change the links to the files without actually needing to change the names of the files every time something is updated? We do that by changing the version number at the end of the file, e.g., `theme-style.css?ver=1.5` might become `theme-style.css?ver=1.6` after a theme update. When we change the version number, we change the link to the file, which tells visiting web browsers and your CDN to fetch the newest copy of the file.

That `?ver=1.6` portion is the "Query String". If we removed that query string--as many speed testing services recommend--then your WordPress site wouldn't function properly. Your visitors would end up seeing old versions of your site!

It's for this reason that ZenCache does not remove query strings from static resources--doing so would essentially break your WordPress site.