---
title: How does the Auto-Cache Engine cache child blogs in a Multisite Network?
categories: questions
tags: auto-cache-engine, wp-multisite
author: raamdev
github-issue:
github-issue: https://github.com/websharks/zencache-kb/issues/84
---

On a Multisite Network the Auto-Cache Engine runs for the main site, and also for each child blog in the network. That occurs without any additional configuration. As it runs through each of the sites, it constructs a URL that it uses to try and find a sitemap for that particular child blog, using whatever you've configured as the global sitemap filename path in **Dashboard → ZenCache → Plugin Options → Auto-Cache Engine**.

![2015-07-30_21-08-58](https://cloud.githubusercontent.com/assets/53005/8998729/3c1f6f40-36ff-11e5-885a-fd755226701c.png)

If you've left the default configuration (i.e., `/sitemap.xml`), the Auto-Cache Engine will check `/sitemap.xml` for the main site (e.g., `http://example.com/sitemap.xml`) and then it will check `/sitemap.xml` for each of the child blogs (e.g., `http://example.com/child1/sitemap.xml`, `http://example.com/child2/sitemap.xml`, etc.). 

If you have changed the name/path of the Sitemap file in the Auto-Cache Engine configuration, the Auto-Cache Engine will use that file/path for each of child blogs instead. 

That means if you've changed the name/path to, for example, `/sitemaps/map.xml`, the Auto-Cache Engine will check `/sitemaps/map.xml` for the main site (e.g., `http://example.com/sitemaps/map.xml`) and then it will check `/sitemaps/map.xml` for each of the child blogs (e.g., `http://example.com/child1/sitemaps/map.xml`, `http://example.com/child1/sitemaps/map.xml`, etc.).