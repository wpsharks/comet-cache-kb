---
title: Recommended Nginx Configuration for ZenCache
categories: tutorials
tags: nginx, static-cdn-filters, installation-upgrading
author: raamdev
github-issue:
github-issue: https://github.com/websharks/zencache-kb/issues/91
---

```nginx
server {

  # ↓ See: http://nginx.org/en/docs/http/ngx_http_core_module.html#etag
  # This reduces load on your server by supporting the If-Modified-Since header,
  # since by browsers for static resources.

  etag on;
  expires 7d;
  if_modified_since before;

  # ↓ See: http://nginx.org/en/docs/http/ngx_http_gzip_module.html#gzip
  # This enables GZIP compression in Nginx, making all static
  # resources load faster in browsers.

  gzip on;
  gzip_vary on;
  gzip_comp_level 6;
  gzip_types text/plain text/xml image/svg+xml # text/html in core already.
    application/rss+xml application/atom+xml application/xhtml+xml
    text/css application/json application/x-javascript
    application/font-otf application/font-ttf;

  # ↓ See: http://davidwalsh.name/cdn-fonts
  # This prevents cross-domain security issues related to fonts.
  # Only needed if you use Static CDN Filters in ZenCache.

  location ~* \.(?:ttf|ttc|otf|eot|woff|woff2|css|js)$ {
      add_header Access-Control-Allow-Origin *;
  }

  # ↓ This is optional, but suggested. It's a flag to tell ZenCache
  # that you completed this Nginx configuration.

  location ~* \.php$ {
      fastcgi_param WP_NGINX_CONFIG done;
  }
}
```

_**Important Note:** The `server{}` configuration block in this example is incomplete; i.e., it only contains the configuration relevant to improving speed on your site and for the best compatibility with ZenCache. It does not include things like `listen` and `try_files` directives. Please consult the [Nginx documentation](http://nginx.org/en/docs/) if you need help with that part._