---
title: Why does ZenCache show an APC Extension Warning?
categories: questions
tags: error-messages
author: raamdev
github-issue:
github-issue: https://github.com/websharks/zencache-kb/issues/83
---

We discovered several major issues with the APC extension that were resulting in fatal errors on some of our customers' sites. The PHP APC extension is outdated and buggy (the last update to the APC extension was 2012) and the PHP community has since abandoned development of the APC extension in favor of the newer [Opcache extension](http://php.net/manual/en/book.opcache.php). To prevent ZenCache from triggering this bug in APC extension (any plugin that uses Closures in its code can trigger the fatal APC bug), we are now showing a warning message to site owners who try to activate ZenCache on a site that has the old APC extesnion enabled.

Shortly after releasing ZenCache v150626 in June 2015, we began receiving sporadic reports that the new version was resulting in Fatal PHP Errors. However, the issue only seemed to affect a subset of ZenCache users and not everyone. 

After extensive research, we discovered that the issue was related to a bug in PHP's APC extension: [PHP Bug #52144](https://bugs.php.net/bug.php?id=52144).

Despite being outdated and buggy, the PHP APC extension is still commonly enabled by default on web servers that are running older versions of PHP, namely PHP v5.3 and PHP v5.4. (The newer Opcache extension that replaces APC is enabled by default in PHP v5.5+.)

We discovered that the APC extension is more likely to trigger a fatal error when PHP is running code that utilizes a lot of Closures, a newer feature of PHP (but one that is officially included with PHP v5.3 and PHP v5.4). Part of the work that went into ZenCache v150626 was a restructured codebase that more heavily utilizied Closures to improve code performance and manageability. As a result, the restructured codebase increased the likelihood of exposing that existing PHP bug. On some systems, just running more than one WordPress plugin that used Closures in its code increased the likelihood of a fatal error.

Since we can't fix the PHP bug ourselves, and because we want to continue supporting PHP 5.3.2+ and PHP 5.4 (for now, at least), we're simply notifying site owners when we detect that their server is running the outdated and buggy APC extension and providing recommendations for upgrading to something more stable.

![2015-07-10_01-09-25](https://cloud.githubusercontent.com/assets/53005/8612560/5dfc91b6-26a0-11e5-891b-dadd8847bb04.png)

## What is the APC Extension?

APC is an acronym for _Alternative PHP Cache_. It was designed as a free and open opcode cache for PHP with the goal of providing a free, open, and robust framework for caching and optimizing PHP intermediate code. However, it doesn't optimize code well enough for large PHP frameworks like WordPress. (If it did, you wouldn't need ZenCache!)

Disabling the APC extension will have no adverse effects on your site. In fact, since the APC extension is so buggy, you will likely be _improving_ your server by disabling the APC extension!

If you want to use an opcode cache, we recommend using the [Opcache extension](http://php.net/manual/en/book.opcache.php). The APC extension has been replaced by the newer Opcache, which is far more stable and still under active development.

## How can I disable the APC Extension?

Depending on what your web hosting company allows you to do, you may be able to add the following line of code to the top of your `wp-config.php` file, right after the line at the top that says `<?php` to disable the APC extension:

```php
ini_set('apc.cache_by_default', false);
```

If that does not work and you still receive the APC Extension Warning, you'll need to contact your web hosting company and ask them to either disable the PHP APC extension or upgrade your server to PHP 5.5+, which uses the newer and more stable Opcache extension.

## Can I run APC, but tell it to exclude ZenCache?

Yes, you can alter your `php.ini` file to accomplish this. Set the `apc.filters` directive as seen below. This will exclude the Closures in ZenCache; i.e., prevent them from being cached by APC, and thus you avoid at least one bug in APC that is triggered when APC attempts to cache PHP Closures.

```ini
apc.filters = "-.+?/zencache(?:\-pro)?/.+?/closures/.+"
```

_Please remember to restart your web server after making this change._

## What if I can't disable APC or upgrade PHP?

In our tests, not all sites experience the fatal error(s) associated with the APC extension bug. As a last resort, you could tell ZenCache to activate itself anyway (by clicking the link the Dashboard notice that says, "click here to ignore this warning") and ignore the fact that the APC extension is enabled. 

However, we don't recommend doing this because something as simple as installing another WordPress plugin that also uses Closures could suddenly result in fatal errors that break your entire site. On the other hand, it could be that you don't experience any issues at all. If you do experience a fatal error related to ZenCache you'll need to [manually uninstall ZenCache](http://zencache.com/kb-article/how-do-i-uninstall-zencache/#toc-86754ab8) to resolve the issue.

The other option would be to install and run an old version of ZenCache, prior to the improvements made to the codebase utilizing Closures. ZenCache v150409 (released April 9th, 2015) was the last release prior to the codebase improvements. You can download previous versions of ZenCache in the [Release Archive](http://zencache.com/release-archive/).

## Help! I received a Fatal Error!

If you ignore the APC extension Warning and activate ZenCache anyway, you may receive a fatal error like the following:

> PHP Fatal error: Base lambda function for closure not found in...

At this point, you will need to [manually uninstall ZenCache](http://zencache.com/kb-article/how-do-i-uninstall-zencache/#toc-86754ab8) to resolve the issue.
