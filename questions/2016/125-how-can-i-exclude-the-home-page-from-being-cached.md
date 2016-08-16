---
title: How can I exclude the Home Page from being cached?
categories: questions
tags: http-referrer-exclusion-patterns, uri-exclusion-patterns, user-agent-exclusion-patterns
author: renzms
github-issue: https://github.com/websharks/comet-cache-kb/issues/125
---

When using Comet Cache Pro, you can use the URI Exclusion Patterns feature (see **Comet Cache → Plugin Options → URI Exclusion Patterns**) to exclude specific pages on your site from being cached. In some cases, you may only want to exclude the home page.

Using [Watered-Down Regex Syntax](https://cometcache.com/kb-article/watered-down-regex-syntax/), it is possible to set an exclusion that will match at the beginning or end of the URI. The solution here is to use the `^` and `$` chars in the URI Exclusion Patterns panel. 

```
^/exact-match/$
```

In the URI Exclusion Patterns panel (see **Dashboard → Comet Cache → Plugin Options → URI Exclusion Patterns**), using the above Watered Down Regex, you can exclude the home page. 

To exclude only the home page, you'd enter the following as a URI Exclusion:

```
^/$
```


Where: 

- `^` = beginning of the string
- `$` = end of the string


![screen shot 2016-07-29 at 7 23 27 pm](https://cloud.githubusercontent.com/assets/13220018/17246948/f7aec7b0-55c1-11e6-9d09-f2235f2b57fa.png)


The Watered-down Regular Expression syntax is supported in several existing Comet Cache features and makes it possible to fine-tune the Comet Cache configuration to suit your needs. For more information on the Watered-Down Regular Expression Syntax, see [this KB Article](https://cometcache.com/kb-article/watered-down-regex-syntax/).