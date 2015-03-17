---
title: Why are my styles missing and/or images broken after enabling Static CDN Filters?
categories: questions
tags: static-cdn-filters
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/38
toc-enable: off
---

If you just configured and enabled Static CDN Filters with a CDN such as Amazon CloudFront or MaxCDN, and now you're seeing broken images and/or missing styles on your site, then you may have enabled Static CDN Filters before the Distribution was ready.

When you create a Distribution with your CDN provider, it takes up to 15 minutes (in some cases, even longer) for the Distribution to finish setting up. During this time, the Distribution's Status will say something like "In Progress", as seen below when creating an Amazon CloudFront Distribution:

![2015-03-16_21-21-06](https://cloud.githubusercontent.com/assets/53005/6679950/a82c629a-cc26-11e4-86ec-429a4bc0784e.png)

If Static CDN Filters are enabled _before_ the CDN has "Deployed" the Distribution, then your images, CSS files, and JavaScript files will point to the CDN, but the CDN won't be ready to serve them. As a result, the all of those links will be broken.

What you need to do is wait until the Distribution's Status changes to "Deployed". Once the CDN has finished setting up the Distribution, you can enable Static CDN Filters and your images, CSS files, and JavaScript files will be properly served from the CDN.

![2015-03-16_21-21-06](https://cloud.githubusercontent.com/assets/53005/6679715/9e922016-cc22-11e4-83a0-f0148317dca2.png)

### What if the Distribution says "Deployed" but links are still broken?

If you visited your site while the CDN was still setting up the Distribution, you may have cached your site with the broken links in your web browser and now your browser is serving the cached version of the page.

Try clearing your browser's cache and restarting the browser. Then visit your site and refresh the page.

If the links are still broken, you can try starting over from scratch: Create a Distribution on your CDN, wait for it to finish being Deployed, and _then_ copy the CDN Hostname, paste it into the ZenCache Static CDN Filters configuration, and click "Save All Changes".
