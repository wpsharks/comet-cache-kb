---
title: Why doesn't Comet Cache "Eliminate Render Blocking" and move CSS/JS scripts into the footer?
categories: questions
tags: html-compression
author: raamdev
github-issue: https://github.com/websharks/comet-cache-kb/issues/49
toc-enable: off
---

Comet Cache does not move CSS/JS scripts to the footer because there's too much risk of corrupting a site that is using a plugin/theme where the plugin/theme developer expected certain scripts to be in the header (the top of the page). 

Page speed testing services like Google PageSpeed and GTMetrix consider it a performance improvement to have JS/CSS scripts loaded in the footer (at the end of the page) because it allows a web page to start loading _before_ the JS/CSS resources have been loaded. This increases the speed, every-so-slightly, at which a page will appear in the browser as it is loaded.

However, an important point to keep in mind is that speed testing services are often not specifically geared towards WordPress sites--they are simply providing advice applicable to websites in general. WordPress sites are often very dynamic, combining a WordPress theme with many WordPress plugins, each one created by a different developer.

If scripts should (or can) be in footer, they need to be placed in the footer by a site/theme designer or the theme/plugin developer needs to indicate to WordPress that the script they are loading can be loaded in the footer (this is something that WordPress makes possible with the [wp_enqueue_script()](http://codex.wordpress.org/Function_Reference/wp_enqueue_script) function). Comet Cache can come back in later and compress and combine the CSS/JS files and it will obey any load-in-footer settings defined by other plugin/theme developers, but moving them around itself is another matter entirely.

### What would happen if Comet Cache moved all CSS/JS files to the footer?

If Comet Cache forced all CSS/JS files to be moved to the footer of website, Comet Cache would introduce conflicts with many other WordPress plugins/themes. For example, a site owner might install a plugin whose developer expected a CSS/JS file to be loaded in the header, because perhaps the plugin was designed to modify the page layout in some way, or perform some changes to the User Interface (quite common with jQuery et. al.). 

In such a scenario, forcing the scripts to load in the footer would have an adverse side effect: the visitor might see one thing as the page is loading, then something else entirely after the page finishes loading and the script in the footer finally loads and makes changes to the page.

#### A quick example: Inline JavaScript API Calls

In this first code snippet, we're showing how a plugin developer would expect their JavaScript file to be loaded (in the head, i.e., NOT to be moved to the footer, as recommended by page speed testing services). Here we have `<script src="widget-api.js"></script>` in the `<head>`

```html
<!DOCTYPE html>
<html>
<head>
	<title>Example</title>
	<script src="widget-api.js"></script>
</head>
<body>
		<div class="widget">
			<script>displayWidget();</script>
		</div>
	</body>
</html>
```

Now, if we move `<script src="widget-api.js"></script>` to the footer (i.e., change the order so that JavaScript files are loaded in the footer, as recommended by page speed testing services), our HTML would look like this:

```html
<!DOCTYPE html>
<html>
<head>
	<title>Example</title>
</head>
<body>
		<div class="widget">
			<script>displayWidget();</script> <!-- JavaScript error: displayWidget is undefined. -->
		</div>
		<script src="widget-api.js"></script>
	</body>
</html>
```

Here the call to `displayWidget()` will fail because it expects `widget-api.js` to have already been loaded; i.e., it expects `displayWidget()` to exist _before_ it is used. The developer would've expected that the JavaScript file was loaded in the head of the page. If we've moved the JavaScript to the footer page, i.e., _after_ the call to `displayWidget()`, then the code for that function would not be loaded in time.

For this reason it really needs to be determined by the plugin/theme developers where a script can be loaded. If it can be loaded in the footer, then best practice would state that it should be specifically defined as something that can be loaded in the footer, as that would increase performance. However, if Comet Cache provided an option that forced all JS/CSS files to be moved the footer, there could be adverse side effects that may be interpreted by a site owner as a Comet Cache bug ("the problem goes away when I disable Comet Cache").

### How can a Plugin/Theme developer ensure scripts load in the footer?

WordPress has a function used by many theme/plugin developers called: [wp_enqueue_script()](http://codex.wordpress.org/Function_Reference/wp_enqueue_script), and this function accepts an argument called `$in_footer`. If you set this to TRUE (or your theme/plugin developers set this to TRUE), then the Comet Cache HTML Compressor will automatically detect this and there's no need to do anything.

If you're a theme developer and you're not using the [wp_enqueue_script()](http://codex.wordpress.org/Function_Reference/wp_enqueue_script) function (you really should be), or if you're a site owner and you want to specifically define some static resources that the HTML Compressor should move to the footer, see [How can I move CSS/JS scripts into the footer?](https://cometcache.com/kb-article/how-can-i-move-cssjs-scripts-into-the-footer/)
