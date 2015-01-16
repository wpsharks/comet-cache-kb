---
title: What are ".u" directories, e.g., "category.u"?
categories: questions
tags: logged-in-users
author: raamdev
github-issue: https://github.com/websharks/zencache-kb/issues/8
test: 3
---

> I see in my cache directory sub-directories that end in `.u`, such as `/category.u/`; what are those?

The `/category/` sub-directory will be for any cache files for your category archive pages (such as `example.com/category/example-category/`). 

The `/category.u/` sub-directory is for any user-specific cache files for category archive pages. It sounds like you have Logged-In User caching enabled (**Dashboard → Quick Cache → Plugin Options → Logged-In Users**) and this is set to `Yes, and maintain a separate cache for each user`. 

This means that when a logged-in user visits a category archive page, they will have their own cache files generated in a `/category.u/` directory; the cache filename for the user will be `[user-id].html`, where `[user-id]` is their WordPress User ID, e.g., `/category.u/6.html`, if their User ID was `6`.
