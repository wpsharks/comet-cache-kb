---
title: How do I setup Static CDN Filters with KeyCDN?
categories: questions
tags: static-cdn-filters
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/64
toc-enable: off
---

[KeyCDN](https://www.keycdn.com) is an alternative to Amazon CloudFront and MaxCDN that can be integrated with Comet Cache Pro through the Static CDN Filters. To integrate Comet Cache with KeyCDN, you'll need to create a new Zone inside your KeyCDN account with a Zone Type of "Pull" and then supply Comet Cache Pro with the Zone "URL" provided by KeyCDN.

## Step-by-Step: Integrating Comet Cache Pro with KeyCDN

1. Login to your KeyCDN account and create a new Zone by visiting **Zones → New Zone**.  

     In the General Zone Settings, enter a name identifier in the **Zone Name** field (letters and numbers only). This will be added to the Zone URL that KeyCDN generates--if your Zone URL ends up being `example-146b.kxcdn.com`, the `example` portion is what gets entered in the Zone Name field. Set the **Zone Status** to _Active_ and the **Zone Type** to _Pull_. Then click the **Show Advanced Features** checkbox--there is one Advanced Feature we need to change.

     ![2015-04-23_12-53-16](https://cloud.githubusercontent.com/assets/53005/7303124/54868c20-e9bc-11e4-9b60-857ac928ff57.png)

1. Scroll down to the **Pull Zone Settings** section and enter your website URL in the **Origin URL** field. Note that this value should be exactly as it appears on your site. If you use **http://www.example.com**, you should enter `http://www.example.com`. If you use **http://example.com**, you should enter `http://example.com`.

     ![2015-04-23_12-50-56](https://cloud.githubusercontent.com/assets/53005/7303180/b635e43e-e9bc-11e4-8381-121e6bfc11e3.png)

1. Scroll down further to the **Ignore Query String** advanced option and change this to _Disabled_.

     ![2015-04-23_12-50-30](https://cloud.githubusercontent.com/assets/53005/7303222/f6e86a88-e9bc-11e4-847f-2e0b8b4d3faa.png)

1. Save your new Zone by clicking the **Save** button at the bottom.

     ![2015-04-23_13-31-43](https://cloud.githubusercontent.com/assets/53005/7303248/347a1fc2-e9bd-11e4-92b1-54558aed53fc.png)

1. KeyCDN will now deploy your new Zone. This will take a few minutes and you'll see a green progress bar while this is happening. When this process finishes and the green bar goes away, you can copy the URL for the Zone and use that to configure Comet Cache Static CDN Filters in the next step.

     **Important:** You must wait until KeyCDN has finished deploying the Zone before you use it with Comet Cache Pro, otherwise you may end up with broken links on your site.

     ![2015-04-23_12-56-14](https://cloud.githubusercontent.com/assets/53005/7303286/8c738efc-e9bd-11e4-8531-35189cfc7b15.png)

1. Copy the Zone **URL** for the new Zone that you just created (it should look something like `example-146b.kxcdn.com`) and paste that into the **CDN Hostname** field in **WordPress Dashboard → Comet Cache → Plugin Options → Static CDN Filters**. You'll also want to make sure Static CDN Filters is enabled and set to "Yes, I want CDN filters applied".

     ![2015-04-23_13-13-01](https://cloud.githubusercontent.com/assets/53005/7303357/111a3ac0-e9be-11e4-9e9a-452d3968cb98.png)

1. When you're finished, click the **Save All Changes** button at the bottom to save your Comet Cache configuration.

     ![2015-04-23_13-13-33](https://cloud.githubusercontent.com/assets/53005/7303359/12bd867a-e9be-11e4-952e-361cc63441a2.png)

That's it! Comet Cache Pro is now configured with your KeyCDN account. If you logout of your WordPress Dashboard and visit your site, you'll see that all static resources (CSS files, JavaScript files, images, etc.) are loaded with URLs that start with something like `http://example-146b.kxcdn.com/`, which indicates that the Comet Cache Pro CDN Integration is now working.

---

**See Also:**

- [How do Static CDN Filters work?](http://cometcache.com/kb-article/how-do-static-cdn-filters-work/)
- [Introduction to Static CDN Filters](http://cometcache.com/kb-article/introduction-to-static-cdn-filters/)
- [Static CDN Filters for WordPress Multisite Networks](http://cometcache.com/kb-article/static-cdn-filters-for-wordpress-multisite-networks/)
