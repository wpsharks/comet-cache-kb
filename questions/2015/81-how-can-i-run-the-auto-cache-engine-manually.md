---
title: How can I run the Auto-Cache Engine manually?
categories: questions
tags: auto-cache-engine
author: raamdev
toc-enable: off
github-issue: https://github.com/websharks/comet-cache-kb/issues/81
---

The Auto-Cache Engine, when enabled, is scheduled to run every 15 minutes. If you want to run the Auto-Cache Engine manually, or if you want to create your own cron job to define a custom schedule using a plugin such as [WP Crontrol](https://wordpress.org/plugins/wp-crontrol/), you can do so by adding `?comet_cache_auto_cache_cron=1` to the end of your site's URL.

For example, if your site was `example.com`, you could run the Auto-Cache Engine by calling the following URL:

```text
http://example.com/?comet_cache_auto_cache_cron=1
```

If you're setting up a cron job inside the control panel with your web hosting company, you can use a command like the following to call the URL using the cURL program (check with your hosting company for the exact path to `curl`):

```text
/usr/bin/curl http://example.com/?comet_cache_auto_cache_cron=1 -so /dev/null
```

### A few things to keep in mind

- Running the Auto-Cache Engine on your own doesn't change the fact that WordPress will still run it every 15 minutes (unless you specifically disable the Comet Cache cron job entry using a plugin such as [WP Crontrol](https://wordpress.org/plugins/wp-crontrol/)).
- Running the Auto-Cache Engine too often will just result in an overlap. In other words, consider the size of your site, your delay time, max run time, and if it's going to overlap from one process to another you'll want to be sure that you avoid this. Otherwise you will just have a whole bunch of running processes at the same time
