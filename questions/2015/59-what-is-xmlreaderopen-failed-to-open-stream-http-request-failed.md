---
title: 'What is "XMLReader::open() failed to open stream: HTTP request failed"?'
categories: questions
tags: auto-cache-engine, error-messages
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/59
---

**Question:** What is "XMLReader::open() failed to open stream: HTTP request failed"?

**Answer:** It sounds like the server where your website is hosted is misconfigured, or does not allow WordPress to connect to itself. The ZenCache Auto-Cache Engine needs to read your XML Sitemap (e.g., `http://example.com/sitemap.xml`) so that it can find all the pages on your site and cache them.

If ZenCache cannot read the URL to your XML Sitemap, then the Auto-Cache Engine will be unable to function properly. As a result, you may see an error like the following in your error log whenever the Auto-Cache Engine runs:

> [06-Mar-2015 12:03:59 UTC] PHP Warning:  XMLReader::open(http://example.com/sitemap.xml): failed to open stream: HTTP request failed!  in /home/example/public_html/wp-content/plugins/zencache-pro/includes/auto-cache.php on line 233

Please contact your web hosting company and ask them to to help you troubleshoot this server issue. Let them know you're running a WordPress plugin called ZenCache that needs to read your XML Sitemap URL using an HTTP request.
