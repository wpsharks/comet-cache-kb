---
title: How do I prevent Comet Cache from disabling the Akismet comment nonce?
categories: questions
tags: mu-plugins-hacks, themeplugin-developers
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/99
---

Comet Cache automatically disables the Akismet Comment Nonce using [the `akismet_comment_nonce` filter](https://github.com/git-mirror/wordpress-akismet/blob/2.5.6/akismet.php#L333) provided by Akismet, which improves compatibility between Akismet and the page caching functionality provided by Comet Cache. This ensures that pages do not contain time-sensitive `nonce` values that should not be cached.

If you would like to prevent Comet Cache from disabling the Akismet comment nonce, you can use an [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins). Please note, however, that Comet Cache _will never_ cache a page that contains a `akismet_comment_nonce` value, so by preventing Comet Cache from disabling the Akismet comment nonce, you may discover that many pages on your site are no longer being cached.

Create this file and directory: `wp-content/mu-plugins/zc-prevent-akismet-nonce-disable.php`:

```php
<?php
/*
Plugin Name: Prevent Comet Cache from Disabling Akismet Comment Nonce
Description: Prevents Comet Cache from automatically disabling the Akismet comment nonce
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('comet_cache_disable_akismet_comment_nonce', '__return_false');
```
