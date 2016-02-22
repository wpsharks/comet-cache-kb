---
title: What is the recommended Nginx Configuration?
categories: questions
tags: nginx
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/4
---

The Nginx configuration that we recommend for Comet Cache is the same as the configuration recommended for WordPress itself. Please see [the official Nginx and WordPress documentation](http://wiki.nginx.org/WordPress). 

#### A note about the `try_files` statement 

If your Nginx configuration contains the `try_files` statement, you'll want to make sure that it is [configured properly](https://github.com/websharks/comet-cache-kb/issues/2), as we have seen WordPress and Comet Cache issues related to a misconfiguration in this area of the Nginx configuration.
