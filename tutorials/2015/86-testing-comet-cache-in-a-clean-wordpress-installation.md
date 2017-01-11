---
title: Testing Comet Cache in a Clean WordPress Installation
categories: tutorials
tags: troubleshooting
author: patdumond
github-issue: https://github.com/websharks/comet-cache-kb/issues/86
---

## Is it Really a Bug?

We receive many bug reports that are difficult and/or impossible to reproduce on our side of things. A site owner will write to us and say, "feature X is not working as expected". One of our staff will follow-up by testing that specific feature, but the problem doesn't exist on our side. Hmmm... what gives? **How can that be?**

**Reason**: WordPress offers you lots of options! As a site owner you have the ability to mix Comet Cache with other plugins and a theme you like best. So the reason we are unable to reproduce the issue on our side? Your environment is slightly different than ours. Your WordPress installation has different plugins, it has had a different history, and it's probably running with a different theme too. Comet Cache also writes cache files to the server and interacts with other server software quite frequently and your server-side configuration is likely different from ours.

As you can imagine, testing every feature of Comet Cache with every possible combination of plugins, and with each and every theme and server configuration that exists for WordPress — is simply not realistic. **We need common ground! In fact, [our policy](https://wpsharks.com/support-policy) is that we require it :-)**

## Reproduce Problems in a Clean WordPress Environment

Like most WordPress plugins, Comet Cache was created, tested, and tuned on a default installation of WordPress. Therefore, we ask that you refrain from reporting a bug until you have been able to successfully reproduce the bug in a default installation of WordPress; i.e. an installation of WordPress where Comet Cache is the only plugin that has ever been installed; and one where you are using a default theme for WordPress (Twenty Seventeen, Twenty Sixteen, Twenty Fifteen, etc). If you’re using any [Must-Use Plugins](http://codex.wordpress.org/Must_Use_Plugins), please remember to deactivate those as well.

This will allow you to experience the intended behavior. If you find that the bug still exists, please [report it](/support/)! Most of the time though, bugs that exist in a live site cannot be reproduced once Comet Cache is isolated. This is an indication that there is a theme/plugin conflict on your live site.

Starting from a clean installation is key. If you start from a clean installation where Comet Cache behaves as expected, you can begin debugging your installation by adding one plugin and/or theme at a time, until you can successfully reproduce the issue; i.e., identify the conflicting plugin/theme.

## Getting Help with Theme/Plugin Conflicts

If you're integrating Comet Cache into a larger set of themes/plugins, we ask that you seek assistance from an experienced WordPress developer who can do a full review of your site and make the proper recommendations (e.g., helping you resolve conflicts between all plugins working together). If you followed the steps above, you should now have some idea of which plugin/theme combination is causing a problem for you. Please pass that information on to your developer.

## Our Support Policy

Support policy: <https://wpsharks.com/support-policy>

> We will not provide support and/or troubleshooting assistance for any Product which has been integrated with another 3rd-party theme or plugin. If you discover a bug, or an inconsistent behavior with a Product which is integrated into a mixture of other themes/plugins for WordPress, we ask that you start by disabling all other plugins and revert to the default theme for your current version of WordPress.

> If problems persist, even in a default theme for WordPress, and no other plugins are active, we are happy to help. Otherwise, if you are integrating our Products into a larger set of themes/plugins, we ask that you seek assistance from an experienced WordPress developer who can do a full review of your site and make the proper recommendations (e.g., helping you resolve conflicts between all plugins working together).

## How to Report Plugin/Theme Conflicts

If you identify a conflict between Comet Cache and another plugin, we would [love to hear about this](/support/)! While we cannot offer support for other 3rd-party themes/plugins, we do accept feedback. Theme/plugin conflicts are reviewed by our developers on a regular basis, and efforts to enhance compatibility are always underway. Thanks in advance for your patience!
