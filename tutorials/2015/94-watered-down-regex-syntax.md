---
title: Watered-Down Regex Syntax
categories: tutorials
tags: uri-exclusion-patterns,http-referrer-exclusion-patterns,user-agent-exclusion-patterns,html-compression
author: kristineds
github-issue: https://github.com/websharks/comet-cache-kb/issues/94
---

True Regular Expressions (i.e., the full syntax) can be very handy for a variety of reasons. However, it is also quite complex. More complex than what most Comet Cache users need. So for that reason, Comet Cache supports a custom, watered-down version of regex. It can be used in exclusion patterns, custom URLs, and more. This provides a good balance between flexibility and simplicity.

## Where is Watered-Down Regex Supported?

Within Comet Cache, there are many areas that support watered-down regex syntax:

- URI Exclusion Patterns (supports the full syntax)
- HTTP Referrer Exclusion Patterns (supports the full syntax)
- User-Agent Exclusion Patterns (supports the full syntax)
- Auto-Clear XML Sitemap Patterns (`^` and `$` are not accepted)
- Auto-Clear Custom URL Patterns (`^` and `$` are not accepted)
- Clearing a Specific URL Pattern (`^` and `$` are not accepted)

## Watered-Down Regex Syntax

The syntax is parsed as plain text (i.e., what you type is what you get), but the following characters are special. These characters were taken from the original/official Regex syntax, and then modified slightly to behave in the following ways that are useful in Comet Cache:

- `*` = 0 or more characters that are NOT a slash `/`
- `**` = 0 or more characters of any kind, including `/` slashes.
- `^` = beginning of the string _(not supported in all cases, see note below)_.
- `$` = end of the string _(not supported in all cases, see note below)_.

_**NOTE:** The `^` and `$` characters are supported by most Comet Cache features that utilize Watered-Down Regex Syntax. However, there are some notable exceptions; i.e., configuration fields where `^` and `$` will not work._

- `^` and `$` are always on when configuring XML Sitemap Patterns under **Comet Cache → Config Options → Automatic Cache Clearing → Sitemap-Related Options → XML Sitemap Patterns**. Patterns entered there must always match from beginning to end, and for that reason, `^` and `$` are always applied (internally). You should avoid using `^` and `$` when configuring XML Sitemap Patterns.

- `^` and `$` are always on when configuring Auto-Clear Custom URL Patterns under **Comet Cache → Config Options → Automatic Cache Clearing → Misc. Auto-Clear Options → Auto-Clear Custom URL Patterns**. Patterns entered there must always match from beginning to end, and for that reason, `^` and `$` are always applied (internally). You should avoid using `^` and `$` when configuring Auto-Clear Custom URL Patterns.

- `^` and `$` are always on when you attempt to clear a Specific URL using the Specific URL tool from the Comet Cache admin bar menu. Patterns entered there must always match from beginning to end, and for that reason, `^` and `$` are always applied (internally). You should avoid using `^` and `$` when clearing a Specific URL.

## Watered-Down Regex Examples

### Custom URL Examples
See: **Dashboard → Comet Cache → Plugin Options → Automatic Cache Clearing → Misc. Auto-Clear Options → Custom URLs**.

To clear all cache files for URIs under `/blog/` (i.e., all Posts):

```
 /blog/**
```

In this example, adding the syntax `**` will exclude all custom URIs that start with `/blog/` and anything infinitely deep beneath that slug.

-------

### URI Exclusion Examples

See: **Dashboard → Comet Cache → Plugin Options → URI Exclusion Patterns**

If you want to exclude your home page URI, and only the home page URI:

```
^/$
```

---

To exclude a URI that begins with `/members/`, and only _that_ specific URI:

```
^/members/$
```

_**Tip:** There is a difference between `*` and `**`._
_To exclude URIs that start with `/members/` and match anything beneath that slug, infinitely deep, you would use `**` (double asterisk), which matches 0 or more characters of any kind, including `/` slashes._

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

To exclude any URI that simply contains `/member/`or `/members/` or `/member[something]/` in it anywhere:

```
/member*/
```

_Excludes: `/member/`, `/members/`, `/member-groups/`, `/member-info/`, and `/member/groups/` too, because there is no `^` or `$` specified; i.e., the match can occur anywhere in the URI, not necessarily from beginning to end._

---

### Auto-Clear XML Sitemap Pattern Examples

See: **Dashboard → Comet Cache → Plugin Options → Automatic Cache Clearing → Sitemap-Related Options → XML Sitemap Patterns**.

Searches are performed against the `REQUEST_URI`; e.g., a request for `/sitemap.xml` and/or `/sitemap-xyz.xml` are both matched by the pattern: `/sitemap**.xml`. Full URLs _should not_ be used; only the URI (everything that comes after the domain). One pattern per line.

If you want to auto-clear `/sitemap.xml`, `/sitemap-1.xml`, and `/sitemap-2.xml`, you could use a pattern like this:

```text
/sitemap*.xml
```

If you want to auto-clear `/sitemap.xml`, `/sitemap/pages/1.xml`, and `/sitemap/posts/1.xml`, you could use a pattern like this: `/sitemap**.xml`.

```text
/sitemap**.xml
```

---

**A note regarding WP Multisite**: Any domains mapped to the current site are cleared automatically. In other words, if you enter `/sitemap**.xml` (the default value for that field) then whenever the cache is cleared for Child Site A, the following are cleared automatically:

- `http://child-a.example.com/sitemap.xml`
- or: `http://example.com[/base]/child-a/sitemap.xml`
- and/or: `http://[MAPPED DOMAIN]/sitemap.xml` (for each domain mapped to child site A)

---

**A note regarding `^` and `$`**: For XML Sitemap Patterns, `^` and `$` are always on. Patterns must always match from beginning to end, and for that reason, `^` and `$` are always applied (internally). You should avoid using `^` and `$` when configuring XML Sitemap Patterns.

---

### Admin Bar Menu: Clearing "Specific URL" Examples

![Clear Cache Options: Specific URL](https://cloud.githubusercontent.com/assets/53005/11138107/295dcd5e-898c-11e5-9e08-b92899f1edc4.png)

**Note:** If you don't see the Clear Cache Options menu in your Admin Bar, see **Comet Cache → Plugin Options → Manual Cache Clearing**.

To clear the cache for a specific URL, you can define a pattern which can be simple, e.g., any single URL on your site, or a complex pattern which includes the use of wildcard characters.

If you want to clear the cache for your `/my-account` page, regardless of which protocol is used to access the page (e.g., `http://` or `https://`, and regardless of whether or not the URL was accesed using the www or non-www version of the domain, then you can add `**` at the beginning of the URL to create a pattern like this:

```text
**domain.com/my-account
```

![Clear Cache Options: Entering a Specific URL Pattern](https://cloud.githubusercontent.com/assets/53005/11138188/2e232572-898d-11e5-9dde-ec23b340770a.png)


This pattern will match all of these URLs and clear any cache files associated with those URLs:

```text
https://www.domain.com/my-account
https://domain.com/my-account
http://www.domain.com/my-account
```

If you also wanted to match anything that might come _after_ `my-account` (e.g., `my-account/`, `my-account/upgrade/`, etc.), you could simply add another `**` so that the pattern becomes:

```text
**domain.com/my-account**
```

---

To clear the cache for any specific URI that contains `/membership/` or `/memberships/` or `/membership[SOMETHING]/` in it

```text
http://www.domain.com/membership*/
```

---

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

---

**A note regarding `^` and `$`**: When clearing a Specific URL, `^` and `$` are always on. Patterns must always match from beginning to end, and for that reason, `^` and `$` are always applied (internally). You should avoid using `^` and `$` when clearing a Specific UR.




