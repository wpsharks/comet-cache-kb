---
title: How do I disable the Nginx htaccess notice?
categories: questions
tags: static-cdn-filters, mu-plugins-hacks, nginx
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/93
---

If you are running the [Nginx Web Server](http://nginx.org), Comet Cache will show a message inside the plugin options indicating that you must [update your Nginx configuration manually](http://cometcache.com/r/kb-article-recommended-nginx-server-configuration/), as modifying your Nginx server configuration is not something that Comet Cache is allowed to do:

![Comet Cache NGINX Notice](https://cloud.githubusercontent.com/assets/53005/18333934/5cfb401e-7541-11e6-8c1e-0d6190530060.png)

If you've already updated your server with the [recommended Nginx configuration](http://cometcache.com/r/kb-article-recommended-nginx-server-configuration/), then you're all set and you can safely ignore the notice. If you want to get rid of the notice completely, you can create a small [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins) to disable the message.

Create this file and directory: `wp-content/mu-plugins/cc-disable-nginx-htaccess-notice.php`:

```php
<?php
/*
Plugin Name: Disable Comet Cache Nginx htaccess notice
Description: Disables the Nginx htaccess notice on the Dashboard
Author: WebSharks, Inc.
Version: 1.0
Author URI: http://www.websharks-inc.com
*/

add_filter('comet_cache_wp_htaccess_nginx_notice', '__comet_cache_wp_htaccess_nginx_notice', 10, 0);

function __comet_cache_wp_htaccess_nginx_notice() {
	return TRUE; // Yes, disable the Nginx htaccess notice
}

```
