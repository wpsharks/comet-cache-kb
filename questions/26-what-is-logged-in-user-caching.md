---
title: What is Logged-In User Caching?
categories: questions
tags: logged-in-users
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/26
---

_Note: If you haven't yet read [Branched Cache Structure](https://zencache.com/kb-article/what-is-the-branched-cache-structure/), please read that before reading this article. Understanding how the Branched Cache Structure works is a prerequisite to understanding how Logged-In User Caching works._

If you have *Dashboard → ZenCache → Plugin Options → Logged-In Users* set to `Yes (maintain separate cache)`, then ZenCache will maintain a separate cache file for each logged in user. This is what we refer to as _Logged-In User Caching_. 

### How does it work?

Let's say we have a user with User ID `42` who logs in views a post called "Sample Post", which has the following permalink: `http://example.com/2014/05/sample-post/`. 

In this scenario, if ZenCache doesn't find an existing cache file for this user, a new one will be generated, specifically for this user, at the following location:

```
wp-content/cache/quick-cache/cache/http/example-com/2014/05/sample-post.u/42.html
```

You can see here that a new subdirectory (`/sample-post.u/`) was created by appending `.u` to the last part of the permalink. Inside that subdirectory, we'll have the cache file generated for each user (in this case, the cache file for our user with User ID `42` has a "Sample Post" cache file called `42.html`).

The `/sample-post.u/` subdirectory will contain the cache files for each logged-in user who visits that post and each user will be served their own, separate cache file. 

Visitors who are not logged in will be served the `sample-post.html` cache file (as explained in [Branched Cache Structure](https://zencache.com/kb-article/what-is-the-branched-cache-structure/)).
