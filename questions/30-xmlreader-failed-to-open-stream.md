---
title: What is "XMLReader::open() failed to open stream"?
categories: questions
tags: auto-cache-engine
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/30
---

**Question:** What is "XMLReader::open() failed to open stream"?

**Answer:** It sounds like your web host has disabled `allow_url_fopen` in the PHP configuration on your server, which means the ZenCache Auto-Cache Engine will be unable to access the URL to your XML Sitemap (which it uses to figure out which pages it on your site it should generate a cache file for).

As a result, you may see an error like the following in your error log whenever the Auto-Cache Engine runs:

> [Wed Mar 04 23:09:25 2015] [warn] [client 185.114.224.0] mod_fcgid: stderr: PHP Warning: XMLReader::open(http://example.com//sitemap_index.xml) [<a href='xmlreader.open'>xmlreader.open</a>]: failed to open stream: no suitable wrapper could be found in /home/example/www/wp-content/plugins/zencache-pro/includes/auto-cache.php on line 233

Please contact your web host and ask them to enable `allow_url_fopen` in the PHP configuration.

_**Note**: We currently have a feature request open to allow the Auto-Cache Engine to fallback on using cURL when `allow_fopen_url` is disabled. See [#440](https://github.com/websharks/zencache/issues/440) for further details and to cast your vote._
