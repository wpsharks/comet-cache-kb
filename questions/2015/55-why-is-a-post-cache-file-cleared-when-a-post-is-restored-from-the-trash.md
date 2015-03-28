---
title: Why is a post cache file cleared when a post is restored from the trash?
categories: questions
tags: 404-requests
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/55
---

If you restore a Post/Page from the Trash and you see a message about a cache file being cleared for that Post/Page ID, you likely have 404 Request Caching enabled (see **ZenCache → Plugin Options → 404 Requests**).

![2015-03-27_21-20-48](https://cloud.githubusercontent.com/assets/53005/6879280/9176b6d2-d4c7-11e4-9db0-42b72b4811fa.png)

When 404 Request Caching is enabled, a cache file link to the 404 Page cache file is created whenever someone visits a post URL that returns a 404 page. 

What this means is that if you have a post in the Trash and someone tries to visit that Post, ZenCache will create a 404 Cache File link as if it were creating a Post Cache file for that post. When you Restore the Post/Page from the Trash, ZenCache deletes this cache file link to the 404 Page and that's the reason you see a message about a cache file being cleared.