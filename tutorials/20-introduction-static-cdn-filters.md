---
title: Introduction to Static CDN Filters
categories: tutorials
tags: static-cdn-filters
author: jaswsinc
github-issue: https://github.com/websharks/zencache-kb/issues/20
---

https://www.youtube.com/watch?v=CbIN9_W3UK4

## ZenCache Pro: Static CDN Filters

In ZenCache Pro, this feature allows you to serve some and/or ALL static files on your site from a CDN of your choosing. This is made possible through content/URL filters exposed by WordPress and implemented by ZenCache Pro. 

All it requires is that you setup a CDN host name sourced by your WordPress installation domain. You give your CDN host name to ZenCache Pro and it'll do the rest! Super easy, and it doesn't require any DNS changes either. :-) In fact, we think you'll find this is one of the simplest/easiest ways to take advantage of the most popular CDNs.

![Static CDN Filters](http://cdn.websharks-inc.com/zencache/uploads/2015/02/static-cdn-filters.png)

### What's a CDN? 

A CDN is a Content Delivery Network (i.e. a network of optimized servers) designed to cache static resources served from your site (e.g. JS/CSS/images and other static files) onto it's own servers, which are located strategically in various geographic areas around the world. 

Integrating a CDN for static files can dramatically improve the speed and performance of your site, lower the burden on your own server, and reduce latency associated with visitors attempting to access your site from geographic areas of the world that might be very far away from the primary location of your own web servers.

![ncdn_-_cdn](http://cdn.websharks-inc.com/zencache/uploads/2015/02/ncdn-cdn.png)

_"[NCDN - CDN](https://commons.wikimedia.org/wiki/File:NCDN_-_CDN.png#mediaviewer/File:NCDN_-_CDN.png)" by [Kanoha](https://commons.wikimedia.org/w/index.php?title=User:Kanoha&amp;action=edit&amp;redlink=1) - Own work. Licensed under [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0) via [Wikimedia Commons](https://commons.wikimedia.org/wiki/)._

### Which CDNs are Supported by ZenCache?

Nearly all of the most popular CDNs are supported. We recommend [MaxCDN](https://www.maxcdn.com/websharks/) and/or [Amazon CloudFront](http://aws.amazon.com/cloudfront/). However, you'll be happy to know that *any* CDN that can be sourced by a domain name; and which offers you a hostname to deliver files through its network, will work just fine with ZenCache Pro.

_CDNs that require DNS changes (such as CloudFlare) are a bit different. These are generally more difficult to integrate w/ ZenCache Pro, since ZenCache Pro expects you to provide it with a host name (i.e. a host name provided by your CDN). CDNs such as CloudFlare expect you to change your DNS records in order to route traffic through their network first. It's not impossible to get this working w/ ZenCache Pro, but we find it's much easier to integrate Static CDN Filters with companies like MaxCDN or CloudFront. Very reasonable, very simple to setup._

#### Here's what it boils down to...

You signup w/ a CDN of your choosing and create what's known as a Distribution (aka: Zone, or Pull Zone; depending on the CDN that you choose). You specify the source of this distribution as your domain name; i.e. the domain name that your installation of WordPress is running from.

Upon creation, your CDN provides you with a host name for this Distribution (e.g. `d1v41qxxxie0l.cloudfront.net`). Finally, you give that CDN host name (provided by your CDN) to ZenCache Pro. Save your ZenCache Pro options and that's it! :-)

_Note: if your CDN provides you with an option to enable "Query String Forwarding" or "Interpretation of Query Strings", please **do** enable this. Enabling this feature allows ZenCache Pro to handle cache invalidations for you automatically._

#### What about Amazon S3?

Amazon S3 is a file storage service, designed to serve file downloads. It is not designed as a Content Distribution Network (CDN). However, Amazon does have a CDN service and that's called **CloudFront** (which is actually built on top of Amazon S3). The ZenCache Static CDN Filters _do_ integrate with Amazon CloudFront (see [How do I setup Static CDN Filters w/ Amazon CloudFront?](http://zencache.com/kb-article/how-do-i-setup-static-cdn-filters-w-amazon-cloudfront/)).

### Which Files are Served by the CDN?

All static files on your site; everything. Of course, you have a lot of control over this too. ZenCache Pro exposes several configuration options that allow you to whitelist/blacklist certain file extensions and/or certain URIs.

It's flexible enough that it can work with pretty much any combination of themes/plugins you like. In some cases you may need to add blacklist exclusions for certain plugins, but that should be a rare occurrence.

---

**See Also:**

- [How do Static CDN Filters work?](http://zencache.com/kb-article/how-do-static-cdn-filters-work/)
- [Static CDN Filters for WordPress Multisite Networks](http://zencache.com/kb-article/static-cdn-filters-for-wordpress-multisite-networks/)
