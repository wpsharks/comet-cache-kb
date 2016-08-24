---
title: How can I show dynamic content while caching the page?
categories: questions
tags: uri-exclusion-patterns
author: renzms
github-issue: https://github.com/websharks/comet-cache-kb/issues/124
---

Comet Cache is a page caching plugin. That means it captures the output from the server and saves it to a cache file. When the next person comes along, Comet Cache serves the cached file instead of expending server resources by having the page reprocessed.

If you have a widget or a plugin that shows some dynamic content on a page that is being cached (e.g., a Page View Counter widget on the Home Page), what will happen is that Comet Cache will cache the output from the page and serve that cached file to future visitors--the dynamic portion will no longer be dynamic.

There are two ways around this problem:

1. Make sure that your dynamic plugin or widget is using JavaScript to dynamically update itself, using something like an AJAX call to the server. If JavaScript is used to update the dynamic content (a counter, for example), then even when the dynamic content is cached it will continue to update as expected. 

2. Exclude the page with the dynamic content from being cached by Comet Cache. This can be done using the **URI Exclusion Patterns** feature.