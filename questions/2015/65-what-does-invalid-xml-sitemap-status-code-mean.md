---
title: What does "Invalid XML sitemap status code" mean?
categories: questions
tags: auto-cache-engine, error-messages
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/65
---

The ZenCache Auto-Cache Engine uses a Sitemap XML to figure out which pages on your site need to be cached. If ZenCache tries to load the URL to your sitemap and the web server responds with a non-`200` Status Code, then an error message like the following will be generated:

> [23-Apr-2015 02:02:48 UTC] PHP Fatal error:  Uncaught exception 'Exception' with message 'Invalid XML sitemap status code at: `http://www.example.com//sitemap.xml`. Expecting a `200` status. Instead got: `404`.' in /home/example/public_html/wp-content/plugins/zencache-pro/includes/auto-cache.php:224

In this case, we can see by the error message that a `404` error was returned. This indicates that the Sitemap XML file does not exist. If you try visiting the URL to your Sitemap XML file (generally `http://YOURDOMAIN.com/sitemap.xml`; see **WordPress Dashboard → ZenCache → Plugin Options → Auto-Cache Engine → XML Sitemap URL**), you should see the XML Sitemap:

![2015-04-23_23-09-18](https://cloud.githubusercontent.com/assets/53005/7311698/cf3a52f2-ea0d-11e4-901d-2a504af0247f.png)

If you don't see the XML Sitemap page but instead see a 404 Error, you likely don't have any XML Sitemap Plugin installed. We recommend using [Google XML Sitemaps](https://wordpress.org/plugins/google-sitemap-generator/). 

Once you install and activate a Sitemaps plugin and can visit the XML Sitemap address in your web browser, the ZenCache Auto-Cache Engine should have no problem reading the URL and auto-caching your site.
