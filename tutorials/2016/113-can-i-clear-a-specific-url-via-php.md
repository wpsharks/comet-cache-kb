---
title: Clearing a Specific URL via PHP
categories: tutorials
tags: clearing-the-cache
author: jaswsinc
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/113
---

Sometimes it is nice to take more control over the way cache files are cleared. Using PHP functions provided by the Comet Cache plugin is one of the most powerful ways to do that. There are a number of API Functions provided by the Comet Cache plugin. I will mention a few of them below and provide examples of their use.

_**Note:** Before you integrate any of the functions shown below, it's important to remember that much of WordPress is driven by hooks and filters. For that reason, before you call any of these functions, please be sure that the [`init` hook](https://codex.wordpress.org/Plugin_API/Action_Reference/init) has been fired first; i.e., that the Comet Cache plugin has been loaded and it available for use within your code._

---

## Clearing a Specific URL

```php
<?php
comet_cache::clearUrl('http://example.com/path/to/page/');
```

_The above will clear this specific URL from the cache._

## Clearing Multiple URLs Matching a Pattern

The `comet_cache::clearUrl()` function also supports [Watered-Down Regex](https://cometcache.com/kb-article/watered-down-regex-syntax/), which makes it easy to clear multiple URLs matching a pattern that you supply.

```php
<?php
comet_cache::clearUrl('http://example.com/post/**');
```

_Clears all URLs that begin with `http://example.com/post/`_

---

## Clearing a Specific WordPress Post/Page by ID

```php
<?php
comet_cache::clearPost(123);
```

_The above will clear this specific Post ID from the cache._

---

## Clearing a Specific User by User ID

Whenever user-specific caching is enabled in your Comet Cache configuration, each user can be associated with a version of the cache that is served only to that user while they are logged-in. This makes it possible for you to clear the entire cache for that specific user without impacting other visitors to the site, or other users who are also logged into the site.

```php
<?php
comet_cache::clearUser(123);
```

_The above will clear this specific User ID from the cache._

## Clearing Current User

```php
<?php
comet_cache::clearCurrentUser();
```

_The above will clear the current User ID from the cache; i.e., the user who is currently logged into the site whenever this API Function is called upon._
