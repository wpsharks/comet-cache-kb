---
title: How do I setup Static CDN Filters with CDN77?
categories: questions
tags: static-cdn-filters
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/46
toc-enable: off
---
[CDN77](http://www.cdn77.com) is an alternative to Amazon CloudFront and MaxCDN that can be integrated with ZenCache Pro through the Static CDN Filters. To integrate ZenCache with CDN77, you'll need to create an "HTTP CDN Resource" inside your CDN77 account and then supply ZenCache Pro with the "CDN URL" provided by CDN77.

## Step-by-Step: Integrating ZenCache Pro with CDN77

1. Login to your CDN77 account and create a new CDN Resource. (If you already have a CDN77 account, visit **CDN → New CDN Resource** to create a new CDN resource for your site.) Select "HTTP Standard" for the resource type. 

     In the General Settings, enter your domain in the **Origin** field, exactly as it appears on your site. If you use **http://www.example.com**, you should enter `www.example.com`. If you use **http://example.com**, you should enter `example.com`. Note that CDN77 requires that you fill in the **CNAMEs** field, even if you're not going to use that feature (not required by ZenCache Pro). If you're not going to setup a CNAME, you can just add `cdn.` to the front of your domain in that field, as shown in the screenshot below.

     ![2015-03-19_15-26-39](https://cloud.githubusercontent.com/assets/53005/6739104/ee789160-ce4c-11e4-9c56-5e3cf767412c.png)

1. Once the resource has been created, you'll want to visit the **Settings** tab and make sure that **Ignore Query String** is set to `Disabled`. This is the default when creating a new Resource on CDN77, but it's a good idea to double-check, as this must be disabled for ZenCache Pro to work properly.

     ![2015-03-19_14-29-59](https://cloud.githubusercontent.com/assets/53005/6739374/a3944584-ce4e-11e4-9635-337c366b4620.png)

1. Now we need to wait for CDN77 to finish provisioning the new resource. You'll see a message on the **Instructions** tab that tells you it will take 10 - 15 minutes to finish. When that message changes to "You CDN resource was successfully uploaded to all Datacenter locations", you can proceed with configuring ZenCache Pro. 

     **Important:** You must wait until CDN77 has finished provisioning the CDN resource before you use it with ZenCache Pro, otherwise you may end up with broken links on your site.

     ![2015-03-19_15-18-16](https://cloud.githubusercontent.com/assets/53005/6739391/c0e51af0-ce4e-11e4-8aa8-719ef1db1249.png)

1. After 10 - 15 minutes, you can refresh the page and you should see the message has changed to the following. Now we're ready to configure ZenCache Pro.

     ![2015-03-19_14-49-58](https://cloud.githubusercontent.com/assets/53005/6739401/c1a23432-ce4e-11e4-98df-0ea3b09dd60c.png)

1. Copy the **CDN URL** for the new CDN resource that you just created (it should look something like `579346857.r.cdn77.net`) and paste that into the **CDN Hostname** field in **WordPress Dashboard → ZenCache → Plugin Options → Static CDN Filters**. You'll also want to make sure Static CDN Filters is enabled and set to "Yes, I want CDN filters applied".

     ![2015-03-19_15-18-37](https://cloud.githubusercontent.com/assets/53005/6739426/e8fa9e16-ce4e-11e4-89b5-c0f5d741f20f.png)

     ![2015-03-19_15-46-06](https://cloud.githubusercontent.com/assets/53005/6739554/a609b438-ce4f-11e4-9fee-6bd687da8b21.png)

1. When you're finished, click the **Save All Changes** button at the bottom to save your ZenCache configuration.

     ![2015-03-19_15-47-23](https://cloud.githubusercontent.com/assets/53005/6739569/d405e6b8-ce4f-11e4-9461-65290acdab75.png)

That's it! ZenCache Pro is now configured with your CDN77 account. If you logout of your WordPress Dashboard and visit your site, you'll see that all static resources (CSS files, JavaScript files, images, etc.) are loaded with URLs that start with something like `http://579346857.r.cdn77.net/`, which indicates that the ZenCache Pro CDN Integration is now working.
