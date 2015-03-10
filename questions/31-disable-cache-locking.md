---
title: How do I disable cache locking?
categories: questions
tags: error-messages, ac-plugins
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/31
---

ZenCache implements a cache-locking mechanism to improve performance, however on some web hosts it can cause problems, especially with hosts that are using a cloud-based NFS (Network File System). 

If cache locking is failing, you may see an error message like the one below:

```
[10-Mar-2015 07:04:35 UTC] PHP Warning: fopen(/tmp/zencache-54843.lock): failed to open stream: Permission denied in /var/www/example.com/wp-content/plugins/zencache-pro/includes/share.php on line 1938 
[10-Mar-2015 07:04:35 UTC] PHP Fatal error: Uncaught exception 'Exception' with message 'Unable to obtain an exclusive lock.' in /var/www/example.com/wp-content/plugins/zencache-pro/includes/share.php:1939 
```

In such a scenario, you can try disabling cache locking. 

You will need to create a ZenCache Advanced Cache Plugin to disable cache locking. Please create this file and directory: `wp-content/ac-plugins/disable-cache-locking.php`:

```
<?php
if(!defined('WPINC')) // MUST have WordPress.
    exit('Do NOT access this file directly: '.basename(__FILE__));

function disable_cache_locking() 
{
    $ac = $GLOBALS['zencache__advanced_cache']; // See: `advanced-cache.php`.
    $ac->add_filter('zencache\\share_disable_cache_locking', function(){ return TRUE; });
}

disable_cache_locking(); // Run this plugin.
?>
```

Once you create that file inside `wp-content/ac-plugins/`, ZenCache will not do any cache locking. 
