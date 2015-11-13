---
title: How do I disable the Nginx htaccess notice?
categories: questions
tags: static-cdn-filters, mu-plugins-hacks, nginx
author: raamdev
github-issue:
github-issue: https://github.com/websharks/zencache-kb/issues/93
---

If you are running the [Nginx Web Server](http://nginx.org), ZenCache will show a message inside the plugin options indicating that you must [update your Nginx configuration manually](http://zencache.com/r/kb-article-recommended-nginx-server-configuration/), as modifying your Nginx server configuration is not something that ZenCache is allowed to do:

![2015-10-15_12-41-56](https://cloud.githubusercontent.com/assets/53005/10520790/372dcd70-733a-11e5-979f-f0027b1322cd.png)

If you've already updated your server with the [recommended Nginx configuration](http://zencache.com/r/kb-article-recommended-nginx-server-configuration/), then you're all set and you can safely ignore the notice. If you want to get rid of the notice completely, you can create a small [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins) to disable the message.

Create this file and directory: `wp-content/mu-plugins/zc-disable-nginx-htaccess-notice.php`:

```php
<?php
/*
Plugin Name: Disable ZenCache Nginx htaccess notice
Description: Disables the Nginx htaccess notice on the Dashboard
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('zencache_wp_htaccess_nginx_notice', '__zencache_wp_htaccess_nginx_notice', 10, 0);

function __zencache_wp_htaccess_nginx_notice() {
	return TRUE; // Yes, disable the Nginx htaccess notice
}

```
