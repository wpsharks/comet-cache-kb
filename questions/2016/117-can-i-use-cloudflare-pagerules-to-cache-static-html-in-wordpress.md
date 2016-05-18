---
title: Can I use CloudFlare PageRules to cache static HTML in WordPress?
categories: questions
tags: cloudflare
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/117
---

CloudFlare can cache static HTML using their PageRules feature (see [this CloudFlare article](https://support.cloudflare.com/hc/en-us/articles/200172256-How-do-I-cache-static-HTML-)), but from the perspective of WordPress, nothing that WordPress produces is really "static HTML"; it's all dynamic HTML. For that reason, CloudFlare PageRules should not be used to cache WordPress.

Comet Cache _creates_ static HTML versions of the dynamic WordPress output and stores that in a cache file, which then gets served to new visitors, but the only reason that Comet Cache can serve static HTML versions of a WordPress site is that Comet Cache also dynamically integrates with WordPress itself and deletes outdated cache files whenever the dynamic content changes in some way. 

For example, if you modify a published post, publish a new post that appears on the home page, change your WordPress theme, or take any other action that changes what WordPress will display on the site, Comet Cache will automatically detect that event and then clear the necessary cache files so that future visitors are not presented with an old, outdated version of the site.

CloudFlare PageRules for caching static HTML is not designed for dynamic websites like WordPress. It is designed for actual static HTML, where there is nothing dynamic that is producing the HTML. For that reason, CloudFlare PageRules should not be used in a dynamic environment like WordPress.