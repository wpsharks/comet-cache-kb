---
title: Introduction to Dynamic Version Salts
categories: tutorials
tags: dynamic-version-salt, themeplugin-developers
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/21
---

_Note: ZenCache stores its cache files for each page of your site based on the `PROTOCOL://HOST/URI` that it's caching. For more information about how ZenCache builds its cache files, please read [Branched Cache Structure](https://zencache.com/kb-article/what-is-the-branched-cache-structure/)._

_Understanding how ZenCache builds cache files is a prerequisite to understanding how Dynamic Version Salts work; otherwise you will be confused by the details below. :-) Please give [this article](https://zencache.com/kb-article/what-is-the-branched-cache-structure/) a quick look-see before you read further._

## What is a "Dynamic Version Salt"?

A *Dynamic Version Salt* (aka: *Version Salt* — shorter) makes it easy for you to create multiple dynamic variations of the cache. These dynamic variations will be served to visitors who meet the criteria defined by your Version Salt. *~ Yes, that sounds complex (and it can be), but it's actually quite simple in most cases.*

For example, if your Version Salt is a cookie, and a visitor has this cookie (of a certain value) they will see pages which were cached with a Version Salt that was based on that cookie's value. A Version Salt could be just about anything; but a cookie is a good way to demonstrate the power of a Version Salt.

![Dynamic Version Salt](http://cdn.websharks-inc.com/zencache/uploads/2015/02/dynamic-version-salt.png)

## Using a Cookie Value as the Version Salt

Let's pretend that you have a WordPress Post titled *"Funky Chicken"*, with the slug: `funky-chicken` which is being served by your WordPress installation which lives on the `example.com` domain. In this example, let's assume the full URL to this Post is `http://example.com/posts/funky-chicken/`

The main ZenCache storage directory is located here: `/wp-content/cache/zencache`. By default, the cache file for this example Post with the slug `funky-chicken` would be stored and served from the following location (inside the main ZenCache storage directory).

```
.../cache/http/example-com/posts/funky-chicken.html
```

*Nothing special here, this is how ZenCache works. See [Branched Cache Structure](https://zencache.com/kb-article/what-is-the-branched-cache-structure/).*

##### Spicing Things Up (Adding a Version Salt)

Now let's enter the following into the Version Salt field for ZenCache, so that we may create multiple versions of this cache file when we want to; and each of these versions will be based on the value of a cookie named `mycookie`; available from the [PHP Super Global](http://www.php.net/manual/en/features.cookies.php) `$_COOKIE['mycookie']`.

I will enter the following into the Version Salt configuration field provided by ZenCache in the Dashboard. A Version Salt can be a string literal, a PHP expression that produces a string, a PHP Constant that is equal to a string, etc... so long as it results in a string value. An empty string is fine too (i.e. if I don't want to use a Version Salt in some cases).

I will use the following for my Version Salt:

```
(string)@$_COOKIE['mycookie']
```

This forces the value of `$_COOKIE['mycookie']` (which comes from an untrusted source — the visitor's browser) to a [string](http://www.php.net/manual/en/language.types.string.php). If this cookie is not defined for a particular user, it will simply be equal to an empty string; i.e. there is no Version Salt used in a case where the visitor does not have this particular cookie. More importantly though, if the visitor *does* have this cookie, the Version Salt will be filled with the value of that cookie as it exists in the visitor's browser.

So for instance, if the value of `$_COOKIE['mycookie']` is the string `chicken lover 34`, the cache file stored and served for that particular visitor would be altered; i.e. different from the default cache file for visitors without this cookie. The altered cache location for this visitor would be stored and served from here:

```
/cache/http/example-com/posts/funky-chicken.v/chicken-lover-34.html
```

Notice that ZenCache detects the presence of a Version Salt, and automatically appends a `.v` (creating a sub-directory) and a cached variation is stored into the slugified cookie value; i.e. `chicken lover 34` automatically becomes `chicken-lover-34.html` ~ nice!

----

## Environment Variables as a Version Salt

Instead of creating a Version Salt based on a cookie, we could base it on the [User-Agent](http://en.wikipedia.org/wiki/User_agent) that a visitor uses to access the site (i.e. the device they are using). If you wanted to maintain a separate cache file for visitors who came to your site with an iPhone, you could detect the User-Agent string using the [PHP Environment Variable](http://www.php.net/manual/en/reserved.variables.server.php) `$_SERVER['HTTP_USER_AGENT']`. We can tell ZenCache to create a separate version of the cache specifically for iPhone users.

Using the same *"Funky Chicken"* example Post: `http://example.com/posts/funky-chicken/`

I will enter the following into the Version Salt configuration field provided by ZenCache in the Dashboard. Remember, a Version Salt can also be a PHP Expression (very handy). This makes it possible for me to use a [PHP Ternary Expression](http://davidwalsh.name/php-shorthand-if-else-ternary-operators) to achieve what I want. In this case, I want to create a seperate version of the cache that is specifically for users who access the site from their iPhone. I will use the following for my Version Salt:

```
preg_match('/iPhone/i', $_SERVER['HTTP_USER_AGENT']) ? 'iPhones' : ''
```

If the visitor comes to my site from an iPhone, I set the Version Salt to `iPhones`, else I leave it empty (i.e. no Version Salt will be used) and they will get the default cached version of my site. More importantly, if they *are* using an iPhone, they get the version of my site that was cached specifically for iPhone users.

```
/cache/http/example-com/posts/funky-chicken.v/iPhones.html
```

Notice that ZenCache detects the presence of a Version Salt, and automatically appends a `.v` (creating a sub-directory) and a cached variation is stored for my Version Salt; i.e. `iPhones.html` ~ perfect!

## What else can be a 'Version Salt'?

A Version Salt can be a single variable like `$_COOKIE['my_cookie']`, or it can be a combination of multiple variables, like `$_COOKIE['my_cookie'].$_COOKIE['my_other_cookie']`.

When using multiple variables, please separate them with a dot; i.e. [concatenate the strings with PHP](http://www.php.net/manual/en/language.operators.string.php). You could also build a hash if you like (optional); e.g. `md5($_COOKIE['my_cookie'].$_COOKIE['my_other_cookie'])`

Other ideas might include Global Variables or Constants defined inside your [/wp-config.php](http://codex.wordpress.org/Editing_wp-config.php) file. For instance, `$GLOBALS['table_prefix']` is a popular one. Or the WordPress Constant `WPLANG`, or anything else you define yourself inside `/wp-config.php`

*Just be sure that whatever you choose is available early-on; i.e. before ZenCache runs, so that it's available to be used in cache path formulation. For instance, something like `get_current_user_id()` would not work here, as this core WP function is not available to ZenCache when it checks for a Version Salt. If you happen to choose something that is not yet defined when ZenCache runs, you might produce an error on your site. See also, [this line of code in the WP core](https://github.com/WordPress/WordPress/blob/master/wp-settings.php#L64) to learn when ZenCache is loaded by WordPress.*

## Version Salts via "Advanced Cache Plugins"

Version Salt functionality (from a UI perspective) is available only in ZenCache Pro. However, it is possible *(even in the lite version of ZenCache)* to create a Version Salt through the use of an "Advanced Cache Plugin".

Here is an [example plugin file](https://github.com/websharks/zencache/blob/000000-dev/zencache/includes/ac-plugin.example.php) that creates a truly dynamic Version Salt, and this will work perfectly in both the lite and pro versions of ZenCache.

#### Theme/Plugin Developers Integrating w/ ZenCache

If you are a theme or plugin developer that would like to create a dynamic Version Salt that works with your application, please go by the [example plugin file](https://github.com/websharks/zencache/blob/000000-dev/zencache/includes/ac-plugin.example.php). Advanced Cache Plugins (aka: *ac-plugins* — shorter) are the recommended way to integrate your theme/plugin with ZenCache; i.e. when you need to construct cache variations for one reason or another. Feel free to ask questions [here](https://github.com/websharks/zencache/issues) as you work through your integration.

## Why am I getting PHP Notices related to my Version Salt?

A version salt of `$_SESSION['example']` on a site that is running in `WP_DEBUG` mode; will kick back an `E_NOTICE ` from PHP, since this is unique to certain visitors with a session and may not be present at all times. Thus, `$_SESSION['example']` is technically invalid, at least some of the time.

I would suggest `@$_SESSION['example']` as the version salt. Or, even better: 
```
isset($_SESSION['example']) && !empty($_SESSION['example']) ? $_SESSION['example'] : ''
```

Another option would be to define the version salt inside `/wp-config.php` where you have more room to write clean code and build a version salt dynamically. Assign the result of whatever that routine does, to a PHP Constant that would then serve as your version salt.

Example, inside `/wp-config.php`
```
if(isset($_SESSION['example']) && !empty($_SESSION['example']))
    define('MY_VERSION_SALT', $_SESSION['example']);
else define('MY_VERSION_SALT', ''); // Default value.
```
Your ZenCache version salt would then become...
```
MY_VERSION_SALT
```
