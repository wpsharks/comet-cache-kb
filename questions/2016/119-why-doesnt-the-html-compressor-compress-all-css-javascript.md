---
title: Why doesn't the HTML Compressor compress all CSS / JavaScript?
categories: questions
tags: html-compression
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/119
---

Compressing CSS and JavaScript requires abiding by specific rules, standards that define just how compressed the source code can be without breaking it. These standards are how we're able to strip out white space and combine the source code from multiple files to speed things up on your site. However, if a plugin or theme adds CSS or JavaScript to your site that is broken or doesn't follow the standards properly, it has a high probability of causing problems with the HTML Compressor.

In fact, CSS and JavaScript code that does not properly follow standards has a high probability of causing problems with any plugin that attempts to compress CSS / JS, however since each compression plugin may adhere to standards differently or may use different techniques for compression, your results with each plugin may vary. 

The problem with not strictly adhering to standards is that while you might be able to compress or combine that broken source code, the code may not operate as expected. That can lead to strange and even seemingly random issues with your site.

The HTML Compressor does a very good job of detecting and concatenating CSS / JS by looking at the output of the raw HTML and searching for any JavaScript and CSS files that may be included on the page, along with any inline snippets. However, since each site will contain a unique combination of plugins and themes, each possibly adding its own CSS / JS, it's important for the HTML Compressor to include options for excluding specific files and allowing you to disable certain features.

The Comet Cache HTML Compressor includes features for excluding specific CSS / JS files from compression: if you find a specific CSS / JS file added by a plugin or theme is causing problems when compressed, you can exclude that file from compression using the CSS and/or JavaScript Exclusion Patterns feature (see [Watered-Down Regex Syntax](https://cometcache.com/kb-article/watered-down-regex-syntax/) for syntax examples):

![HTML Compressor - CSS / JS Exclusion Patterns](https://cloud.githubusercontent.com/assets/53005/15936522/591c5306-2e39-11e6-9e18-a7c340045f02.png)

There's also a whole slew of HTML Compression options that control various aspects of overall compression. If you're having a problem with the HTML Compressor that cannot be resolved by excluding a specific file, sometimes disabling a specific compression feature will allow you to work around the issue.

![HTML Compression - Options](https://cloud.githubusercontent.com/assets/53005/15936501/4298718c-2e39-11e6-9051-74f12b6d0a9f.png)

A final thing to keep in mind is that not all plugins and themes will be compatible with the Comet Cache HTML Compressor. Comet Cache does a very good job compressing CSS and JS in a way that is reliable, logical, and safe but sometimes there will be scenarios where reliable, logical, and safe do not allow for full compression on your site.

There are other compression plugins that are solely dedicated to compressing static resources. If you're having trouble getting the Comet Cache HTML Compressor to work for you, you can try disabling the HTML Compressor and using another compression plugin, such as [Autoptimize](https://wordpress.org/plugins/autoptimize/).
