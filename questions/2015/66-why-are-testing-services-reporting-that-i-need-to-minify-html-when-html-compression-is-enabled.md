---
title: Why are testing services reporting that I need to Minify HTML when HTML Compression is enabled?
categories: questions
tags: html-compression
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/66
---

If you see a message from a speed testing service, such as Google PageSpeed, reporting that you should "Minify HTML", and you already have Comet Cache Pro HTML Compression enabled, with the _"Yes, compress the final HTML code too."_ enabled (see **WordPress Dashboard → Comet Cache → Plugin Options → HTML Compression**), then you're likely seeing a false-positive report.

First, make sure that you actually have the necessary HTML Compression options enabled:

![2015-04-29_13-00-13](https://cloud.githubusercontent.com/assets/53005/7396559/1e11cec6-ee70-11e4-81e9-a0b9e74e80f8.png)

Even with those compression options enabled, you may still see a message like this from your page speed testing service:

![2015-04-29_12-54-49](https://cloud.githubusercontent.com/assets/53005/7396560/215fbf8e-ee70-11e4-9872-fc5675078eef.png)

However, you will likely notice that the report indicates only a small percentage (7% in the example above) potential reduction being reported.

This is most likely because you have the HTML Notes enabled, to allow you to se that Comet Cache is actually working. With the HTML Notes enabled, you can see information about Comet Cache when you "View Source" on your site. However, these notes include some extra "whitespace", which the page speed testing service is likely reporting:

![2015-04-29_12-50-35](https://cloud.githubusercontent.com/assets/53005/7396607/751b90a8-ee70-11e4-8388-48c144311592.png)

To fix this, simply disable the HTML Notes in **WordPress Dashboard → Comet Cache → Plugin Options → Enable/Disable** by setting the option to _"No, I don't want my source code to contain any of these notes"_:

![Comet Cache: Enable/Disable](https://cloud.githubusercontent.com/assets/7514953/21015890/96f91e44-bd9e-11e6-8ae1-60bda7c8f7fe.png)
