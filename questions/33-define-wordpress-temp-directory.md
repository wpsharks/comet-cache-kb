---
title: How do I define a WordPress temp directory?
categories: questions
tags: error-messages
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/33
toc-enable: off
---

If your web host prevents WordPress from opening files in `/tmp/` (a common default temp directory for PHP), then you may receive an error like the following:

> [10-Mar-2015 07:04:35 UTC] PHP Warning: fopen(/tmp/comet-cache-54843.lock): failed to open stream: Permission denied in /var/www/example.com/wp-content/plugins/comet-cache-pro/includes/share.php on line 1938
> [10-Mar-2015 07:04:35 UTC] PHP Fatal error: Uncaught exception 'Exception' with message 'Unable to obtain an exclusive lock.' in /var/www/example.com/wp-content/plugins/comet-cache-pro/includes/share.php:1939 

To fix this, you can define a custom temp directory specifically for WordPress and then give that custom temp directory write permissions (e.g., `755` or `777`).

#### Creating and defining a custom WordPress temp directory

1. Create a custom temp directory, for example `wp-content/temp/`
1. Give that custom temp directory permission for WordPress to write to (e.g., `755` or `777`)
1. Tell WordPress to use your custom temp directory by adding the following to `wp-config.php`:

```
define('WP_TEMP_DIR','/home/username/www/wp-content/temp');
```

_Note: Replace `/home/username/www/wp-content/temp` with the full path to the temp directory on your server. Also, note that the line should be added above the line that says `/* That's all, stop editing! Happy blogging. */`_

You can read more on the WordPress Codex about [Changing File Permissions](http://codex.wordpress.org/Changing_File_Permissions). If you need help creating the temp directory, setting file permissions, or updating your `wp-config.php` file, please contact your web host.
