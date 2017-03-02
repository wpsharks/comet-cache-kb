---
title: Debugging Auto-Clear Routines
categories: tutorials
tags: themeplugin-developers
author: raamdev
github-issue:
github-issue: https://github.com/websharks/comet-cache-kb/issues/132
---

Comet Cache attaches to many hooks in WordPress using the [WordPress Plugin API](https://codex.wordpress.org/Plugin_API) to catch various events that occur so that Comet Cache can automatically clear the cache at the appropriate time. This makes it possible for Comet Cache to ensure that the cache on your site stays up-to-date and that an old (stale) cache is never served to visitors.

If you find that the cache is being cleared unexpectedly for some reason, you might have another plugin that is firing a hook that Comet Cache attaches to. The best way to figure out what's happening is to place a logging routine inside the appropriate Comet Cache function, so that when the Auto-Clear routine is fired, a debug trace is logged to a file that you can review. 

**NOTE: This article is provided only as an example of how a developer might locate what piece of code outside of Comet Cache is triggering a Comet Cache Auto-Clear routine. If you're not comfortable modifying source code, please consult with a developer.** 

## Locating the Proper Auto-Clear Function

There are many Auto-Clear functions in Comet Cache, some specialized and some more general. For example, [`autoClearHomePageCache()`](https://github.com/websharks/comet-cache/blob/170220/src/includes/traits/Plugin/WcpHomeBlogUtils.php#L8-L47) is used to clear the Home Page cache and [`autoClearPostCache()`](https://github.com/websharks/comet-cache/blob/170220/src/includes/traits/Plugin/WcpPostUtils.php#L8-L112) is used when clearing the cache for a specific Post.

The Auto-Clear routines are in several different files, but you'll note that they all start with `Wcp` and they're all located in `src/includes/traits/Plugin/`. 

## Adding the Logging Routine

Once you've located the specific Auto-Clear routine that you want to debug, you'll need to add a logging routine just before the `return` statement at the end of the function (e.g., [here](https://github.com/websharks/comet-cache/blob/170220/src/includes/traits/Plugin/WcpHomeBlogUtils.php#L45)). 

Here's the logging routine:

```php
// ------------- START LOGGING ROUTINE -------------

$e = new \Exception();
$trace = explode("\n", $e->getTraceAsString());
$trace = array_reverse($trace);
array_shift($trace); // remove {main}
$length = count($trace);
$result = array();
for ($i = 0; $i < $length; $i++)
{
     $result[] = ($i + 1)  . ')' . substr($trace[$i], strpos($trace[$i], ' ')); // replace '#someNum' with '$i)', set the right ordering
}
    
$debug = "\t" . implode("\n\t", $result);

file_put_contents(WP_CONTENT_DIR.'/comet-cache-debug.log', $debug."\n\n"."\n\n----------------------------\n\n", FILE_APPEND);

// ------------- END LOGGING ROUTINE -------------
```

Now whenever that routine runs, you'll find an entry in `wp-content/comet-cache-debug.log` that looks something like this:

```
----------------------------

1) /app/src/wp-admin/post.php(193): edit_post()
2) /app/src/wp-admin/includes/post.php(378): wp_update_post(Array)
3) /app/src/wp-includes/post.php(3578): wp_insert_post(Array, false)
4) /app/src/wp-includes/post.php(3402): clean_post_cache(Object(WP_Post))
5) /app/src/wp-includes/post.php(5714): do_action('clean_post_cach...', 9, Object(WP_Post))
6) /app/src/wp-includes/plugin.php(453): WP_Hook->do_action(Array)
7) /app/src/wp-includes/class-wp-hook.php(323): WP_Hook->apply_filters('', Array)
8) /app/src/wp-includes/class-wp-hook.php(300): WebSharks\CometCache\Classes\Plugin->autoClearPostCache(9)
9) /app/src/wp-content/plugins/comet-cache/src/includes/traits/Plugin/WcpPostUtils.php(100): WebSharks\CometCache\Classes\Plugin->autoClearHomePageCache()

----------------------------
```

That entry shows the specific series of events that led to the routine being called. In this case, we can see that WordPress fired the `edit_post` hook (in this example, I simply edited a post from the WordPress Dashboard), which then called `wp_update_post()`, and so on until the Comet Cache `autoClearHomePageCache()` function was called to clear the Home Page cache.

This output should help you determine exactly what is calling the Comet Cache Auto-Clear routine that you're trying to debug.

## Cleaning Up

When you're finished debugging, you should remove the debugging lines that you added and delete the `wp-content/comet-cache-debug.log` log file.