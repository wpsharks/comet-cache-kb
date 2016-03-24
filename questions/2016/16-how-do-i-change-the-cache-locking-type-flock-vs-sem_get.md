---
title: How do I change the cache locking type?
categories: questions
tags: cache-locking
author: jaswsinc
github-issue: https://github.com/websharks/comet-cache-kb/issues/16
---

**See also, this primer:** [What is cache locking?](https://cometcache.com/kb-article/what-is-cache-locking/)

---

## How do I change the cache locking type?

If you are experiencing `rename()` errors, or other PHP errors (PHP Exceptions) related to a race-condition; it could be attributed to file/directory locking. The concept of locking the cache directory and/or specific files in the cache directory is precisely what prevents race conditions and/or directory rename failures in Comet Cache.

By default, Comet Cache uses the popular [flock](http://linux.die.net/man/2/flock) strategy, as this works across the widest range of servers. Since `flock` requires no special PHP extensions to work effectively, it is easiest way for Comet Cache to accomplish file locking.

However, if your server supports `sem_get()` (see: <http://php.net/manual/en/book.sem.php>) you can tell Comet Cache to use a Semaphore instead. On some hosting platforms, the use of `flock()` may not work as expected (e.g., if you use NFS or a server cluster). Therefore, if you are having trouble, please [install the Semaphore extension for PHP](http://php.net/manual/en/sem.installation.php), and then make the following change to your Comet Cache installation.

Create this directory and file:
`wp-content/mu-plugins/cc-cache-lock-type.php`

```php
<?php
add_filter('comet_cache_cache_lock_type', function(){
    return 'sem';
});
```
