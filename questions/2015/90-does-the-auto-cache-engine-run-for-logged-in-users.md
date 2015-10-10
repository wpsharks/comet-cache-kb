---
title: Does the Auto-Cache Engine run for logged-in users?
categories: questions
tags: auto-cache-engine
author: raamdev
github-issue:
github-issue: https://github.com/websharks/zencache-kb/issues/90
---

The Auto-Cache Engine (**Dashboard → ZenCache → Plugin Options → Auto-Cache Engine**) is designed to pre-cache your site, that is to generate cache files ahead of time so that visitors don't have to wait for the cache file to be generated if they are the first to visit a page.

When Logged-In User Caching is enabled (**Dashboard → ZenCache → Plugin Options → Logged-In Users**), ZenCache will maintain a separate cache for each user that logs into your site. However, **the Auto-Cache Engine will not generate cache files for logged-in users** because doing so would require that the Auto-Cache Engine login as each user on your site, and then visit each page on your site to generate a cache file for that user. That is simply not practical as it does not scale.

The Auto-Cache Engine will only cache pages that non-logged-in visitors can see, as per your XML Sitemap and/or your List of URLs to Auto-Cache.