---
title: Why are cache files not being cleared after the expiration time?
categories: questions
tags: directory-expiration-time
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/56
toc-enable: off
---

An expiration time does not determine when the cache files are cleared from the filesystem. The expiration time simply determines the maximum age a cache file can have before a request for that cache file will result in the cache file being regenerated.

ZenCache only checks the cache file expiration time when it is about to serve the cache file to a visitor. If ZenCache determines the cache file is past its expiration time (i.e., it has lived past the maximum age configured in **ZenCache → Plugin Options → Directory / Expiration Time**), it will regenerate the cache file and serve the new version to the visitor.

### A Quick Example

Let's say you have **ZenCache → Plugin Options → Directory / Expiration Time** set to 15 minutes and you have a page at `http://example.com/my-page/`. 

A cache file is generated the first time someone visits `http://example.com/my-page/`. Now let's say 20 minutes goes by (5 minutes past the expiration time) and nobody has visited the page again. 

That (now expired) cache file will still exist on the filesystem. However, since it has expired (it's older than the expiration time of 15 minutes) it will never be served to a visitor. 

Instead, the next time someone visits `http://example.com/my-page/`, ZenCache will detect that the cache file for that page has expired and it will regenerate the cache file, creating a new one and replacing the old one.