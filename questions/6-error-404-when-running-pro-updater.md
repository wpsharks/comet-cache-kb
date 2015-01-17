---
title: Why am I getting a 404 error when running the Pro Updater?
categories: questions
tags: plugin-updater
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/6
---

**Question:** When I try to update ZenCache Pro, I am forwarded to a page that says "No Such Page Found". ZenCache Pro will not update from automatic Plugin Updater. The only way I'm able to update is to download the update, remove the old plugin, and re-install. What is the problem with the Plugin Updater?

**Answer:** If you're getting a 404 error when attempting to run the Quick Cache Pro Updater, you most likely have software on your server blocking the request to the WebSharks update server. The most common culprit is Apache's ModSecurity module.

Please contact your web host with the following request, which should disable the particular ModSecurity rule that often causes issues with the Quick Cache Pro Updater:

> I run a WordPress plugin called Quick Cache Pro and its updater requires that ModSecurity rule #340163 be whitelisted/disabled for my domain. Can you please whitelist/disable ModSecurity rule #340163?
