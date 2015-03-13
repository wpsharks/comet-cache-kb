---
title: How can I disable the Quick Cache deprecated notice?
categories: questions
tags: error-messages
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/37
---

Now that Quick Cache is no longer being maintained, a deprecated notice appears in the Options panel:

![2015-03-13_17-24-52](https://cloud.githubusercontent.com/assets/53005/6648190/46e2bfb4-c9ad-11e4-974d-fb93cf302de4.png)

If you choose to continue using Quick Cache and you want to disable the deprecated notice, you can add the following code to an [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins) or to your theme's `functions.php` file:

```
add_filter('quick_cache_show_deprecated_notice', '__quick_cache_show_deprecated_notice', 10, 0);
function __quick_cache_show_deprecated_notice() {
	return FALSE; // Disable the deprecated notice
}
```