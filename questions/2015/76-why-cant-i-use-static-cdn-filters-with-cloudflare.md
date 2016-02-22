---
title: Why can't I use Static CDN Filters with CloudFlare?
categories: questions
tags: static-cdn-filters, cloudflare
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/76
toc-enable: off
---

Unlike traditional CDNs (such as Amazon CloudFront or MaxCDN), CloudFlare is unique in that it requires redirecting your entire site to the CloudFlare servers, which takes place when you change your DNS settings to point your site to CloudFlare (a required step in setting up CloudFlare).

Most CDNs do not require changing your DNS settings. Instead, they require that you change the URLs on your static resources so that they point to the CDN. With traditional CDNs (such as Amazon CloudFront or MaxCDN), the Comet Cache Static CDN Filters handles the rewriting of all your static resource URLs to point the static resource URLs at the CDN.

With CloudFlare, however, _all requests to your site_ (including requests for non-static resources) get sent through CloudFlare. By the time the request gets to WordPress (and therefore to Comet Cache), the request has already gone through CloudFlare and any static resources have already been cached. That means if you're using CloudFlare, there's no need (no point, really) in configuring the Comet Cache Static CDN Filters, since rewriting the URLs for your static resources would be pointless (those resources have already been cached by CloudFlare).

## Do I even need Comet Cache if I'm using CloudFlare?

CloudFlare can cache static resources, but it can't speed up WordPress by reducing database queries through intelligent page caching. That's where Comet Cache comes in. Comet Cache is a WordPress caching plugin, so its primary job is to speed up WordPress so that each page is loaded as fast as possible. CloudFlare has no direct access to WordPress, so it cannot do anything about speeding up WordPress itself.

When you're using CloudFlare, all of the primary Comet Cache features (with the exception of Static CDN Filters) are still very relevant and will contribute to speeding up your WordPress site. With CloudFlare + Comet Cache, you can get the best of both worlds: the security and convenience of a managed CDNfrom CloudFlare plus the intelligent page caching features from Comet Cache that speeds up WordPress.

## How do other WordPress caching plugins 'support' CloudFlare?

You may have seen other WordPress caching plugins that mention that they "support CloudFlare". All that really means is that they provide options inside the plugin to control your CloudFlare settings (the same settings you can change by logging into your CloudFlare account). There's no static resource caching-specific integration that is possible between WordPress and CloudFlare due to the way CloudFlare works.

_Note: We're in the process of adding support for controlling your CloudFlare settings from directly within Comet Cache. See [Issue #418](https://github.com/websharks/comet-cache/issues/418)._
