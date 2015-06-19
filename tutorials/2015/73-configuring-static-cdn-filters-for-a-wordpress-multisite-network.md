---
title: Configuring Static CDN Filters for a WordPress Multisite Network
categories: tutorials
tags: static-cdn-filters, wp-multisite
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/73
---

The ZenCache Static CDN Filters are fully compatible with WordPress Multisite Networks and this KB Article will outline a few common Multisite Network scenarios and offer suggestions for how to configure the Static CDN Filters for your specific scenario. 

The three common WordPress Multisite Network scenarios are Multisite with Sub-Directories (for which you can configure a single CDN Domain Name, or multiple CDN Domain Names to take advantage of Domain Sharding), Multisite with Sub-Domains, and Multisite with Domain Mapping.

## WordPress Multisite w/ Sub-Directories

This is the default configuration when you first setup a WordPress Multisite Network. When running in sub-directory mode, your child sites all reside under the same top-level domain, e.g., `http://example.com/child-site1/`, `http://example.com/child-site2/`, etc.

If your Multisite Network is running with Sub-Directories, you only have a single domain that needs to be connected to the CDN (the top-level domain). However, you can still take advantage of [Domain Sharding](http://zencache.com/r/domain-sharding/) and define multiple CDN domain names (an advanced configuration that requires configuring CNAMEs through your web hosting company).

### Option 1: Single CDN Domain Name

![2015-05-21_20-10-15](https://cloud.githubusercontent.com/assets/53005/7761586/717a62f8-fff5-11e4-834b-d374d5871755.png)

### Option 2: Multiple CDN Domain Names

When you're running a WordPress Multisite Network in sub-directory mode, the only reason you would configure multiple CDN domain names is to take advantage of [Domain Sharding](http://zencache.com/r/domain-sharding/).

![2015-06-19_17-49-36](https://cloud.githubusercontent.com/assets/53005/8263737/c3a8bcc4-16ab-11e5-85d9-92f0f020ae90.png)

Domain Sharing allows you distribute your static resources to multiple CDN domain names, thereby increasing performance by working around concurrency limits in popular browsers; i.e., making it possible for browsers to download many more resources simultaneously, resulting in a faster overall completion time. 

## WordPress Multisite w/ Sub-Domains

If you are running a WordPress Multisite Network with Sub-Domains, you can define a list of sub-domains with their corresponding CDN hostname. ZenCache will then use the respective CDN hostname when rewriting static resource URLs on that sub-domain.

If you only want to enable the Static CDN Filters for the primary domain (e.g., `example.com`), then you can simply specify a primary domain CDN mapping and skip the sub-domain mappings.

![2015-05-21_14-27-07](https://cloud.githubusercontent.com/assets/1563559/7760212/7f0a4378-ffc5-11e4-8191-c9b2f06e7d17.png)

## WordPress Multisite w/ Domain Mapping

If you're using Domain Mapping and you want to enable Static CDN Filters on the mapped domains, simply supply a list of mapped domains with their corresponding CDN hostname.

If you only want to enable the Static CDN Filters for the primary domain (e.g., `example.com`), then you can simply specify a primary domain CDN mapping and skip the sub-domain mappings.

![2015-05-21_14-28-29](https://cloud.githubusercontent.com/assets/1563559/7760226/aeacc920-ffc5-11e4-9f49-f8037db4f48a.png)
