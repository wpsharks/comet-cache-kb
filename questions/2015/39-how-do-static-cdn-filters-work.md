---
title: How do Static CDN Filters work?
categories: questions
tags: static-cdn-filters
author: jaswsinc
github-issue: https://github.com/websharks/zencache-kb/issues/39
---

When you enable ZenCache Static CDN Filters (**ZenCache → Plugin Options → Static CDN Filters**) and configure ZenCache with a CDN of your choosing, ZenCache will replace (filter) all links to static resources on your site so that they point to the CDN, instead of pointing at your server. 

Static CDN Filters can greatly reduce the load on your server as all static resources (e.g., images, CSS files, JavaScript files) will be loaded from the CDN instead of being loaded from your server. A static resource will only be loaded from your server one time (so that the CDN can cache it).

If static resources change on your server (such as when you upgrade WordPress or change your theme), ZenCache will tell the CDN to fetch a new copy of the static resource so that the cache remains up-to-date.

## How It Works (the Technical Details)

Whenever you create an Amazon Distribution or a MaxCDN Pull Zone (each CDN has its own terminology, but for this article we'll use Amazon CloudFront as an example), this is how it works:

<div class="li-margins"></div>

- You create a Distribution (aka: Pull Zone) that is configured to pull files from a particular HTTP host name; e.g., `www.mysite.com`. In other words, your site (`www.mysite.com`) becomes the underlying source for the CDN to pull from.
- The CDN gives you a host name that references the CDN Distribution you created; e.g., `xxxxxxx.cloudfront.net`.
- You give this CDN Host Name to ZenCache.
- ZenCache will then change the host name in all static resources served by your WordPress installation. So intead of WordPress serving `www.mysite.com/my-image.png`, it will start linking to static resources using `xxxxxxxx.cloudfront.net/my-image.png?iv=1`

![zencache-static-cdn-filters-enable-disable](https://cloud.githubusercontent.com/assets/53005/6723895/46153582-cdc5-11e4-9b17-b82bdf399a6f.png)

What happens next occurs on the CDN side. Whenever `xxxxxxxx.cloudfront.net/my-image.png?iv=1` is accessed for the first time, your CDN visits `www.mysite.com/my-image.png` silently behind-the-scenes. It pulls the file from your server (the "Origin ServeR") and caches it across its global network of servers (Edge Locations); and then it serves the file as expected. Future requests for `xxxxxxxx.cloudfront.net/my-image.png?iv=1` are much faster, because the CDN has already cached it.

Changing `xxxxxxxx.cloudfront.net/my-image.png?iv=1` to `xxxxxxxx.cloudfront.net/my-image.png?iv=2` (i.e., changing the `?iv=1` part of the URL to `?iv=2`) alters the resource URL, which forces the CDN to pull the file from your server again whenever that altered URL is accessed for the first time. Thus, whenever ZenCache needs to update the CDN cache, it simply bumps the internal `?iv` counter by 1.

![zencache-static-cdn-filters-diagram](https://cloud.githubusercontent.com/assets/53005/6723898/47a2d062-cdc5-11e4-8933-ed0133a9fc08.png)

### Does it take time for files to propagate in the CDN (to Edge locations)? How long?

No, this happens almost instantly; i.e., it occurs whenever a file is accessed for the first time (as mentioned above). Most site owners (and/or visitors) never notice that this even occurs. For all practical purposes it is simply cached in real-time. Very much the same way that ZenCache itself caches pages on your WordPress site. The CDN pulls the file from your server when it is accessed for the first time, and then serves it. Future requests are even faster because the file is already cached by this time.

### What are the "Misses" reported by CloudFront or other CDN? 

Hits and Misses are normal. The easiest way to explain this is by looking at the CloudFront docs on [CloudFront Cache Statistics Reports](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cache-statistics.html):

> **Hit** – A viewer request for which the object is served from a CloudFront edge cache. In access logs, these are requests for which the value of x-edge-result-type is Hit.

> **Miss** – A viewer request for which the object isn't currently in an edge cache, so CloudFront must get the object from your origin. In access logs, these are requests for which the value of x-edge-result-type is Miss.

> **Error** – A viewer request that resulted in an error, so CloudFront didn't serve the object. In access logs, these are requests for which the value of x-edge-result-type is Error, LimitExceeded, or CapacityExceeded.

> The chart does not include refresh hits—requests for objects that are in the edge cache but that have expired. In access logs, refresh hits are requests for which the value of x-edge-result-type is RefreshHit.

If you're using a different CDN provider, you should check the documentation on their website for further details.

### I'm seeing 10%+ "Errors" reported on the CDN; is this normal?

Hits and Misses are normal behavior; i.e., expected to occur. Errors not so much. Based on a `10%`+ error report I'd say that you are running into trouble somewhere. Perhaps with a configured limit, or a problem with connectivity between your site and the CDN servers. 

You should check your Apache error logs for any communication failures that have occurred whenever the CDN attempted to cache a static file. If you need assistance with this, please contact your web hosting company.
