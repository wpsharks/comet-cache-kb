---
title: How do I setup Static CDN Filters w/ Amazon CloudFront?
categories: questions
tags: static-cdn-filters
author: jaswsinc
github-issue: https://github.com/websharks/comet-cache-kb/issues/19
toc-enable: off
---

https://www.youtube.com/watch?v=zxMTFixyP18

## Do I need to change my DNS?

No, you do not need to change any DNS settings when using Amazon CloudFront, that is unless you choose to use an Alternative Domain Name (see below). By default, Amazon CloudFront associates a `cloudfront.net` domain name with your CloudFront distribtuion (e.g., `d111111abcdef8.cloudfront.net`). The easiest way to configure the Static CDN Filters is to just use this auto-generated domain. 

However, if you want to associate your CloudFront distribution with your own domain name (e.g., `cdn.example.com`), see the Amazon CloudFront documentation for [Using Alternate Domain Names (CNAMEs)](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html). Once you've set up an alternate domain name for your CloudFront distribution, you can configure the Comet Cache Static CDN Filters with that alternate domain.

### See also:

- [Introduction to Static CDN Filters](http://cometcache.com/kb-article/introduction-to-static-cdn-filters/)
- [How do Static CDN Filters work?](http://cometcache.com/kb-article/how-do-static-cdn-filters-work/)
- [Static CDN Filters for WordPress Multisite Networks](http://cometcache.com/kb-article/static-cdn-filters-for-wordpress-multisite-networks/)
