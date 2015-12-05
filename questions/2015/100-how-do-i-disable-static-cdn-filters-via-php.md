---
title: How do I disable Static CDN Filters via PHP?
categories: questions
tags: static-cdn-filters, mu-plugins-hacks, themeplugin-developers
author: raamdev
github-issue:
github-issue: https://github.com/websharks/zencache-kb/issues/100
---

The ZenCache Pro Static CDN Filters do not run in the shutdown phase like the caching engine does, which means that reliably disabling Static CDN Filters by setting the `ZENCACHE_ALLOWED` or `DONOTCACHEPAGE` constants is not possible.

The ZenCache caching engine will always obey the `ZENCACHE_ALLOWED` and `DONOTCACHEPAGE` constants for disabling page caching, but since the Static CDN Filters are not currently mixed with the caching engine (for performance reasons), you cannot always rely on those constants to disable Static CDN Filters.

If you absolutely need to disable Static CDN Filters programmatically, you can use an [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins).

Create this file and directory: `wp-content/mu-plugins/zc-disable-static-cdn-filters.php`:

```php
<?php
/*
Plugin Name: Disable ZenCache Static CDN Filters via PHP
Description: Disables ZenCache Static CDN Filters via PHP
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

<?php
add_filter('zencache_options', function($options) {
    if(is_page('my-page')) {
        $options['cdn_enable'] = '0';
    }
    return $options;
});
```
