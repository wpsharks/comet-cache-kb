---
title: What is the Branched Cache Structure?
categories: questions
tags: dynamic-version-salt
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/23
---
Comet Cache stores cache files for each page on your site based on the `PROTOCOL://HOST/URI` that it's caching, inside the default Comet Cache cache directory located at `wp-content/cache/comet-cache/cache/`. This builds the cache using a logical 'branched cache structure', based on the structure of the pages on your site.

To see how this works, let's assume we have a post called "Sample Post" at the following URL: `http://example.com/2014/05/sample-post/`. When someone visits that URL, Comet Cache will parse out the following parts using the PHP superglobals `$_SERVER['HTTPS']`, `$_SERVER['HTTP_HOST']`, `$_SERVER['REQUEST_URI']`:

- **URL**: `http://example.com/2014/05/sample-post/`
- **PROTOCOL**: `http`
- **HOST**: `example.com`
- **URI**: `/2014/05/sample-post/`

From that information, Comet Cache will first check if there is an existing cache file to serve for that page. If none is found, it will build the cache file path, starting with the Comet Cache cache location (`wp-content/cache/comet-cache/cache/`) and creating any necessary subdirectories to reflect the path of the URI.

In our example, the following subdirectories are created: `/http/`, `/example-com/`, `/2014/`, and `/05/`, to give us a final cache path of:

```
wp-content/cache/comet-cache/cache/http/example-com/2014/05/
```

*Note: Several special characters (such as periods) are replaced with hyphens when building the cache path, so `example.com` becomes `example-com`.)*

The cache file for "Sample Post" is then written to a file called `sample-post.html`, where `sample-post` is the last portion of the URI.

We then end up with the following cache file:

```
wp-content/cache/comet-cache/cache/http/example-com/2014/05/sample-post.html
```

Comet Cache then loads and displays that cache file to each new visitor.
