---
title: Watered-Down Regex Syntax
categories: tutorials
tags: uri-exclusion-patterns,http-referrer-exclusion-patterns,user-agent-exclusion-patterns,html-compression
author: kristineds
github-issue: https://github.com/websharks/zencache-kb/issues/94
---

True Regular Expressions (i.e., the full syntax) can be very handy for a variety of reasons. However, it is also quite complex. More complex than what most ZenCache users need. So for that reason, ZenCache supports a custom, watered-down version of regex. It can be used in exclusion patterns, custom URLs, and more. This provides a good balance between flexibility and simplicity.

## Watered-Down Regex Syntax

The syntax is parsed as plain text (i.e., what you type is what you get), but the following characters are special. These characters were taken from the original/official Regex syntax, and then modified slightly to behave in the following ways that are useful in ZenCache:

- `*` = 0 or more characters that are NOT a slash `/`
- `**` = 0 or more characters of any kind, including `/` slashes
- `^` = beginning of the string 
- `$` = end of the string

The following sections provide specific examples for each place within ZenCache that the syntax can be used.

---

## Where is Watered-Down Regex supported in ZenCache?

Within ZenCache, there are many areas that support watered-down regex syntax:

- Custom URLs
- URI Exclusion
- HTTP Referrer Exclusion
- User-Agent Exclusion
- Sitemap URI
- Specific URL 

## Watered-Down Regex Examples

### Custom URL Examples
See: **Dashboard → ZenCache → Plugin Options → Automatic Cache Clearing → Misc. Auto-Clear Options → Custom URLs**.

To clear all cache files for URIs under `/blog/` (i.e., all Posts):

```
 /blog/**
```

In this example, adding the syntax `**` will exclude all custom URIs that start with `/blog/` and anything infinitely deep beneath that slug.

-------

### URI/Referer/User-Agent Exclusion Examples

See: **Dashboard → ZenCache → Plugin Options → URI Exclusion Patterns/HTTP Referrer Exclusion Patterns/User-Agent Exclusion Patterns**.

For instance, if I want to exclude only the home page URI:

```
^/$
```

---

To exclude a URI that begins with `/members/`, and only _that_ specific URI:

```
^/members/$
```

---

Note the difference between `*` and `**`. To exclude URIs that start with `/members/` and anything beneath that slug, infinitely deep:

```
^/members/**
```

_Excludes: `/members/`, `/members/jason/`, `/members/jason/profile/`, `/members/groups/a/`, `/members/groups/b/c/a/edit`, etc._

---

To exclude `/members/` and anything beneath that slug, **one** level deep:

```
^/members/$
^/members/*/$
```

_Excludes: `/members/`, `/members/jason/`, `/members/groups/`; but NOT `/members/groups/a/`_

---

To exclude any URI that simply contains `/members/` in it anywhere:

```
/members/
```

---

To exclude any URI that simply contains `/member/`or `/members/` or `/member[SOMETHING]/` in it anywhere:

```
/member*/
```

_Excludes: `/member/`, `/members/`, `/member-groups/`, `/member-info/`, and `/member/groups/` too, because there is no `^` or `$` specified._

-------

### Sitemap URI Examples

See: **Dashboard → ZenCache → Plugin Options → Automatic Cache Clearing → Sitemap-Related Options → XML Sitemap Patterns**.

If you want to clear URLs for a mapped domain, the URLs that you list should include the mapped domain. To cover all domains if you need to:

```text
http://*/path/to/something/
```

**NOTE:** The scheme (i.e., `http://` or `https://` is ignored), and both schemes are cleared automatically.

-------

### Clear Cache "Specific URL" Examples

See: **ZenCache → Plugin Options → Manual Cache Clearing**.

To clear the cache for a specific URL, you can define a pattern which can be simple, i.e. single URL, or complex which includes the use of wildcard characters.

If you want to clear the cache for your `/my-account` page, regardless of which protocol is used to access the page (e.g., `http://` or `https://`, and regardless of using www or non-www, then you can add `**` at the beginning of the URL:

```text
**domain.com/my-account
```

This pattern will match all of these URLs:

```text
https://www.domain.com/my-account
https://domain.com/my-account
http://www.domain.com/my-account
```

If you also wanted to match anything that might come after `my-account` (e.g., `my-account/`, `my-account/upgrade/`, etc.), you could simply add another `**` so that the pattern becomes:

```text
**domain.com/my-account**
```

-------

To clear the cache for any specific URI that contains `/membership/` or `/memberships/` or `/membership[SOMETHING]/` in it

```text
http://www.domain.com/membership*/
```

-------

To clear the cache for `/membership/` and any pages or posts beneath it, one level deep, add `*` at the end of the URL:


``` text
http://www.domain.com/membership/*
```

This will clear cache for the following URLs:

```text
http://www.domain.com/membership/pageA/
http://www.domain.com/membership/postB/
http://www.domain.com/membership/group/
```
