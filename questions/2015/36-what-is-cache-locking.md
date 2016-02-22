---
title: What is Cache Locking?
categories: questions
tags: cache-locking
author: jaswsinc
github-issue: https://github.com/websharks/comet-cache-kb/issues/36
---

## Cache Locking Explained

Imagine for a moment that you _just_ installed Comet Cache; i.e., nothing is cached yet, but it's about to be. Now, the easiest way to explain what cache locking is, is to think about a scenario where multiple people are hitting a single page at the exact same time. In a case like this, there are actually two (or more) server processes running together simultaneously.

To keep this example simple, let's pretend there are just two server processes. One of these will have the job of taking the HTML output from WordPress, creating a cache file, and writing to that cache file; i.e., building/priming the cache. This way future visitors hitting this page will be served the cached copy. The other server process should yield to the other, but both visitors need to see the output of course.

Hmm, but wait. If there are two (or more) server processes running at exactly the same, which one of these does the cache writing, and which one yields to the other? This is what a "lock" is for. The first server process to obtain an exclusive write-lock (i.e., a lock on a particular cache file) will win. Keep in mind that we are talking about microseconds here.

So it's this lock that makes it possible for a decision to be made. If there were no decision, both server processes would attempt to write the cache file at the exact same time, and this is what can lead to a corruption of the cache; i.e., one process will eventually time it just right, and manage to overwrite the work that another process is doing. In some cases this can even result in PHP error messages. We want to avoid that, and this is why a lock is necessary.

## Wait, Isn't There a Better Way?

There are some choices (each with their own ups and downs), but no, not really a better way at the moment. A lock needs to be established when we are dealing with a filesystem. It's a common issue actually, and the concept of an exclusive lock (aka: write lock, or "cache lock" in the case of Comet Cache) is something that many software applications deal with.

Atomic disk writes; i.e., using a temp file followed by a rename when performing disk writes has shown to be most effective at preventing race conditions, and it's the fastest, easiest, and most efficient way to deal with such a scenario—in our experience. However, there are a few cases when atomic disk writes are simply not enough on their own; and this is where a mutually exclusive lock must be obtained on the entire cache directory, not just on a single file. One example is when Comet Cache is clearing or purging the cache directory. More on this below.

## Cache Locked While Clearing/Purging

Comet Cache recently enhanced a portion of its codebase that deals with cache clearing/purging, and since there are now so many of these operations that can occur _while_ traffic is still hitting the front-end of a site; i.e., _while_ we are purging/clearing a temporary copy of the cache directory; there is a need for an exclusive lock during the few seconds when this occurs. We want to avoid a race condition on very busy sites. A cache lock allows Comet Cache to do that.

For example, if we are purging files in a temporary copy of the cache directory from the back-end, we need to lock the cache directory on the front-end while this occurs. This process takes just a few seconds (usually less than one-tenth of a second), but that's still enough time for a problem to arise on a very busy site. It's not enough to _just_ use the temp file + rename methodology on its own. It needs to be coupled with an exclusive lock on the entire cache directory if we are to achieve perfection.

## Cache Locking Techniques

Comet Cache supports two different locking techniques:

<div class="li-margins"></div>
- `sem_get()`; i.e., Semaphores. The benefits of this technique are speed, performance, and that its functionality is better suited to our use case; i.e., Semaphores are part of a system that is specifically designed for the sort of locking that we need. It is also (generally speaking) easier to work with across different types of filesystems. e.g., Hosting companies may choose to alter their implementation slightly to make Semaphores more reliable with a specific cloud-based architecture they use.

  _In order to use `sem_get()`, your installation of PHP must be compiled with the System V Semaphore extension. See: [System V IPC family of functions](http://php.net/manual/en/intro.sem.php) and [installation instructions](http://php.net/manual/en/sem.installation.php). See also: [How do I change the cache locking type?](https://github.com/websharks/comet-cache-kb/issues/16)_
- `flock()`; i.e., Advisory File Locking (**Comet Cache default**). The benefits associated with this technique are compatibility and simplicity. In most cases, `flock()` is the best choice, because it does not require that PHP be compiled with support for Semaphores, and `flock()` is available across all Linux distros, and even works on Windows servers too.

  However, it is slightly less flexible when it comes to how much control that a hosting company (or server administrator) will have. Also, the use of `flock()` is really intended for specific files, not to lock an entire directory or a multiprocess application. It is also slightly slower, but not a huge difference in our tests. Overall, it's a very good alternative to Semaphores, and since it is a simpler/cleaner way to lock a mutex file, there are cases when it might even be preferred over `sem_get()`, even though it is technically less flexible than Semaphores are.

## How Do I Decide Which Technique is Right for Me?

Ask your hosting company. Refer them to this article and explain that you have two options: `sem_get()` or `flock()`. Which do they suggest? A good hosting company will know exactly what you're referring to. You might even browse through their knowledge base for tips related to this topic.

Ultimately, the advice presented by your hosting company _should_ be followed (highly recommended). Having said that, nearly _all_ hosting companies support `flock()`. If in doubt, the default choice i.e., `flock()`,  should work just fine for you :-)

## How Can I Choose the Locking Technique I Prefer?

Please see: [How do I change the cache locking type?](https://github.com/websharks/comet-cache-kb/issues/16)
