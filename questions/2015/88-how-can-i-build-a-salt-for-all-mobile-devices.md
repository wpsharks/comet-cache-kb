---
title: How can I build a salt for all mobile devices?
categories: questions
tags: dynamic-version-salt
author: jaswsinc
github-issue: https://github.com/websharks/zencache-kb/issues/88
---

If your site is "Adaptive" (i.e., serves an entirely different version of the site to mobile devices), you might need to split your cache into one or more partitions. This is accomplished by using a Version Salt.

_**Consider:** If your site is "Responsive", you shouldn't need to do this, because the same version of the site is served to all visitors. In short, CSS (i.e., Responsive design) takes care of mobile viewport issues automatically. Responsive design is generally recommended over an Adaptive design._

---

In the following example, we identify any type of mobile device. A Version Salt splits the cache into two parts. Mobile and _not_ mobile. If your site serves content in a different way, for each different mobile device, you might need to adjust this a bit further. The example should give you a good starting point.

---

### Step 1: Generating the Salt for Mobile Device Detection

Create this directory and file:
`/path/to/wordpress/zc-is-mobile.php`

_**Note:** This file should reside in the same directory as `/wp-config.php`_

```php
<?php
function zc_is_mobile() {
	static $salt = null;
	if ( isset( $salt ) ) {
		return $salt;
	}
	if ( empty($_SERVER['HTTP_USER_AGENT']) ) {
		$salt = '';
	} elseif ( strpos($_SERVER['HTTP_USER_AGENT'], 'Mobile') !== false // many mobile devices (all iPhone, iPad, etc.)
		|| strpos($_SERVER['HTTP_USER_AGENT'], 'Android') !== false
		|| strpos($_SERVER['HTTP_USER_AGENT'], 'Silk/') !== false
		|| strpos($_SERVER['HTTP_USER_AGENT'], 'Kindle') !== false
		|| strpos($_SERVER['HTTP_USER_AGENT'], 'BlackBerry') !== false
		|| strpos($_SERVER['HTTP_USER_AGENT'], 'Opera Mini') !== false
		|| strpos($_SERVER['HTTP_USER_AGENT'], 'Opera Mobi') !== false ) {
			$salt = 'mobile';
	} else {
		$salt = '';
	}
	return $salt;
}
```

---

### Step 2: Include `zc-is-mobile.php` in your `wp-config.php`

Edit your `/wp-config.php` file and add this line somewhere before the call that includes `/wp-settings.php`. The point being, we want this function to be available for ZenCache to use in the early phase of the caching process.

```php
require_once(ABSPATH . 'zc-is-mobile.php');
```

![2015-09-08_17-31-20](https://cloud.githubusercontent.com/assets/1563559/9751301/76909464-564f-11e5-923c-418b7e2ff481.png)

---

### Step 3: Define Version Salt in Dashboard

Here we tell ZenCache to use the `zc_is_mobile()` return value as the Version Salt. Thus, if it's a mobile device, the Version Salt becomes the word `mobile`. If it's not, the Version Salt is empty. This effectively splits the cache into two parts. Mobile and _not_ mobile.

![2015-09-08_17-29-04](https://cloud.githubusercontent.com/assets/1563559/9751276/30fd8ef2-564f-11e5-9bdb-4507fbfabe5e.png)