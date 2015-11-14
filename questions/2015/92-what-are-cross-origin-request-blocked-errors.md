---
title: What are Cross-Origin Request Blocked Errors?
categories: questions
tags: static-cdn-filters
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/92
toc-enable: off
---

Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from which the resource originated. If you are using ZenCache Static CDN Filters and some of your website fonts are not loading, this may be the result of a Cross-origin Request Blocked error like the following:

![2015-11-13_19-06-39](https://cloud.githubusercontent.com/assets/53005/11160591/c842ee60-8a39-11e5-9195-207e20061481.png)

To resolve this issue, your server must send an `Access-Control-Allow-Origin` header. The way to do this is by adding a snippet to your root `.htaccess` file (Apache) or by manually updating your server configuration (Nginx).

### Apache (automatically configured)

If you are running the Apache web server, ZenCache will attempt to update your `.htaccess` file with the following rules automatically when you enable Static CDN Filters, but here is the snippet for your reference:

```apache
<IfModule headers_module>
  <FilesMatch "\.(ttf|ttc|otf|eot|woff|woff2|font.css|css|js)$">
    Header set Access-Control-Allow-Origin "*"
  </FilesMatch>
</IfModule>
```

### Nginx (manual configuration required)

If you are running the Nginx web server, then you cannot use `.htaccess` rules and will need to manually update your Nginx configuration file with the following:

```nginx
location ~* \.(?:ttf|ttc|otf|eot|woff|woff2|css|js)$ {
    add_header Access-Control-Allow-Origin *;
  }
```

## What if setting the header doesn't work?

In our research, we have found that some CDNs cache the initial header request received by your server, so if you made this change to your server configuration _after_ enabling Static CDN Filters, you will likely need to create a new CDN Hostname at your CDN provider and reconfigure ZenCache Static CDN Filters with that new hostname. That way the CDN can see the new `Access-Control-Allow-Origin` header that your server is sending.

If you're still having issues, please check your CDN provider for advanced options related to Forwarding Headers for the CDN Hostname. For example, with Amazon CloudFront you can specifically Whitelist the `Access-Control-Allow-Origin` header to make sure that Amazon CloudFront picks up that header from your server:

![2015-11-13_19-19-45](https://cloud.githubusercontent.com/assets/53005/11160733/1157f9ae-8a3c-11e5-9be9-9b1694b20022.png)
