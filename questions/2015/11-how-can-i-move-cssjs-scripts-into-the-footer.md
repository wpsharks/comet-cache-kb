---
title: How can I move CSS/JS scripts into the footer?
categories: questions
tags: html-compression
author: jaswsinc
github-issue: https://github.com/websharks/comet-cache-kb/issues/11
toc-enable: off
---
The HTML Compressor will not move the resources that it finds (see [Why doesn't Comet Cache move CSS/JS scripts into the footer?](https://cometcache.com/kb-article/why-doesnt-comet-cache-eliminate-render-blocking-and-move-cssjs-scripts-into-the-footer/)). This means that if the original resources were in the `<head>`, they remain in the `<head>` section after compression/consolidation also. 

This is to avoid a scenario where moving resources into another location could introduce conflicts in the way these JavaScript resources are used in other parts of the page; i.e. the HTML Compressor does not make a decision about where to put the JavaScript resources, only in how they are compressed and combined together in the original location where they were found.

Many site owners prefer to place `<script>` tags at the bottom of their page in accordance with suggestions introduced by Pingdom and Google Page Speed testing tools. If you decide to do this, please do so before the HTML Compressor runs. Also, to make it clear to the HTML Compressor, please wrap all of your Footer Scripts into the following HTML comment tags for clarity during parsing: `<!-- footer-scripts --><!-- footer-scripts -->`

If you don't wrap your scripts inside `<!-- footer-scripts --><!-- footer-scripts -->`, the HTML Compressor just treats these as Inline Scripts like any other JavaScript it would find in the body. That's not nearly as beneficial, so always wrap Footer Scripts.

```
<!-- footer-scripts -->
<script type="text/javascript" src="//..."></script>
<script type="text/javascript" src="//..."></script>
<script type="text/javascript" src="//..."></script>
<script type="text/javascript" src="//..."></script>
<!-- footer-scripts -->
```

**DEVELOPER TIP:** In WordPress, there is a function used by many theme/plugin developers called: [wp_enqueue_script](http://codex.wordpress.org/Function_Reference/wp_enqueue_script), and this function accepts an argument called `$in_footer`. If you set this to TRUE (or your theme/plugin developers set this to TRUE), then the HTML Compressor can automatically detect this and there's no need to wrap Footer Scripts inside `<!-- footer-scripts -->` on your own.
