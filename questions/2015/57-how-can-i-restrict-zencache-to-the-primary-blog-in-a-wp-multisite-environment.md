---
title: How can I restrict ZenCache to the Primary Blog in a WP Multisite Environment?
categories: questions
tags: mu-plugins-hacks
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/57
toc-enable: off
---

When ZenCache is installed in a WordPress Multisite Environment, it must be Network Activated. This results in ZenCache being enabled on all sites in the Multisite Network. If you want to restrict ZenCache so that it's only enabled on the Primary Blog, you can use an [MU-Plugin](http://codex.wordpress.org/Must_Use_Plugins).

Create the following file and directory: `wp-content/mu-plugins/zc-restrict-to-primary-blog.php`

```php
<?php
add_action('init', function()
{
    if(!is_multisite())
        return; // Not applicable.

    if(!defined('DOMAIN_CURRENT_SITE'))
        return; // Not possible.

    if(!defined('PATH_CURRENT_SITE'))
        return; // Not possible.

    if(strcasecmp($GLOBALS['current_blog']->domain, DOMAIN_CURRENT_SITE) !== 0)
        define('ZENCACHE_ALLOWED', FALSE);

    else if(strcasecmp($GLOBALS['current_blog']->path, PATH_CURRENT_SITE) !== 0)
        define('ZENCACHE_ALLOWED', FALSE);
});
```

### How do I know ZenCache has been disabled on the Child Blogs?

If you visit a Child Blog (while logged out of WordPress, as Logged-In User Caching is disabled by default) and "View Source" on one of the Child Blog pages, you should see a message like this at the bottom:

![2015-03-28_13-05-41](https://cloud.githubusercontent.com/assets/53005/6881964/52977ecc-d54b-11e4-9e81-fc48370b71f6.png)

This indicates that the MU-Plugin is working and limiting ZenCache to the Primary Blog.

### How do I hide the ZenCache HTML Notes?

You can disable the HTML Notes in **WordPress Dashboard → ZenCache → Plugin Options → Enable/Disable**.