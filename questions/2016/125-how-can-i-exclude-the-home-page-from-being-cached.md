---
title: How can I exclude the Home Page from being cached?
categories: questions
tags: http-referrer-exclusion-patterns, uri-exclusion-patterns, user-agent-exclusion-patterns
author: renzms
github-issue: https://github.com/websharks/comet-cache-kb/issues/125
---

The URI Exclusion Patterns feature (see **Comet Cache → Plugin Options → URI Exclusion Patterns**) can be used to exclude specific pages on your site from being cached, including the Home Page.

Using the powerful [Watered-Down Regular Expression Syntax](https://cometcache.com/kb-article/watered-down-regex-syntax/), it is possible to define an exclusion pattern that will match the beginning of a URI _and_ the end of a URI. In the URI Exclusion Patterns panel (see **Dashboard → Comet Cache → Plugin Options → URI Exclusion Patterns**), we'll enter a pattern that will tell Comet Cache to exclude the home page from being cached. 

To exclude only the home page, enter the following as a URI Exclusion:

```
^/$
```


**Explanation of pattern**: 

- `^` = beginning of the string
- `/` = a literal slash character
- `$` = end of the string

This pattern says to match any URI that starts and ends with a slash, which means that it's the home page.

![URI Exclusion Patterns: Exclude Home Page](https://cloud.githubusercontent.com/assets/13220018/17246948/f7aec7b0-55c1-11e6-9d09-f2235f2b57fa.png)


The Watered-down Regular Expression syntax is supported in several existing Comet Cache features and makes it possible to fine-tune the Comet Cache configuration to suit your needs. For more information on the Watered-Down Regular Expression Syntax, see [this KB Article](https://cometcache.com/kb-article/watered-down-regex-syntax/).
