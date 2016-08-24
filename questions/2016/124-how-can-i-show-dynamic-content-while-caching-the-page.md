---
title: How can I show dynamic content while caching the page?
categories: questions
tags: uri-exclusion-patterns
author: renzms
github-issue: https://github.com/websharks/comet-cache-kb/issues/124
---

Comet Cache is a page caching plugin. That means it captures the output from the server and saves it to a cache file. When the next visitor comes along, Comet Cache serves the cached file instead of expending server resources by having the page reprocessed. 

If you have a widget or a plugin that shows some dynamic content on a page that is being cached (e.g., a Page View Counter widget on the Home Page), what will happen is that Comet Cache will cache the output from the page and serve that cached file to future visitors—the dynamic portion will no longer be dynamic.

There are two ways around this problem:

1. Make sure that your dynamic plugin or widget is using JavaScript to dynamically update itself, using something like an AJAX call to the server. If JavaScript is used to update the dynamic content (a counter, for example), then even when the dynamic content is cached it will continue to update as expected because JavaScript runs on the client-side (in the browser) instead of on the server, which means that even if the page is cached on the server, the JavaScript will remain dynamic. This is the ideal way to make dynamic content compatible with page caching plugins.

2. Exclude the page with the dynamic content from being cached by Comet Cache. This can be done using URI Exclusion Patterns to specify the URI to the page with the content that needs to remain dynamic (see **Comet Cache → Plugin Options → URI Exclusion Patterns**).

While it's certainly _possible_ to support dynamic fragmentation, where a page is cached while a portion of the page remains dynamic, such a feature has both security and performance issues and for that reason Comet Cache does not support dynamic fragmentation at this time. If you'd like to vote for this feature or provide feedback, please see [this feature request](https://github.com/websharks/comet-cache/issues/222).
