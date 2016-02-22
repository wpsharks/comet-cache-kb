---
title: Does Comet Cache clear the CDN cache?
categories: questions
tags: static-cdn-filters
author: jaswsinc
github-issue: https://github.com/websharks/comet-cache-kb/issues/40
toc-enable: off
---

No, Comet Cache does not clear the CDN cache. The Comet Cache cache (stored on the local filesystem) and the CDN cache are separate. Comet Cache will only clear the local cache that it creates (i.e., in `wp-content/cache/comet-cache/`). The CDN cache is created and stored on the CDN side.

Generally speaking, a CDN cache _only_ needs to be refreshed whenever a theme or plugin is upgraded. Comet Cache listens for these events (i.e., theme/plugin updates) and automatically tells the CDN to fetch and cache a new copy of the file whenever files are altered. CDNs refer to this as "invalidating a cached file".

The events that Comet Cache listens for and considers as events worth invalidating an existing CDN cache

- WordPress is updated.
- A WP theme is updated.
- A WP plugin is updated.

Comet Cache will tell the CDN that the file has changed (i.e., been invalidated) by incrementing the `?iv=` variable that Comet Cache attaches to each URL cached by the CDN. In this way, Comet Cache can tell the CDN that a particular cached file has changed and therefore the CDN should request a new copy and throw away the old cached copy.

It is also possible to clear the cache on the CDN side on your own. In the case of CloudFront, you can perform Invalidations, and other CDNs provide similar functionality. You'll need to check with your CDN provider to see if they offer an option to purge the CDN cache from their Dashboard. Note, however, that doing this manually is unnecessary (it won't hurt, but it's unnecessary), as Comet Cache handles invalidations on its own.

For more information on Amazon CloudFront Invalidations, see [CloudFront :: Invalidating Objects](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html)

### Does the CDN ever purge files on its own?

Yes. Most CDNs have a expiration date that you can configure. When a cached file on the CDN has been around longer than the configured expiration date, the CDN will expire (throw away) the file and fetch a new copy.

Most CDNs will be configured to do this based on the `Expires:` header that your server sends. So for instance, if your server sends an `Expires:` header for JS/CSS/images, that's how long the CDN will cache it until it fetches it from your server again.

---

**See also:**

- [How do Static CDN Filters work?](http://cometcache.com/kb-article/how-do-static-cdn-filters-work/)
