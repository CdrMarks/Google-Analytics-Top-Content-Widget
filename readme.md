# Google Analytics Top Content Widget #

**Contributors:** jtsternberg  
**Plugin Name:**  Google Analytics Top Content Widget  
**Plugin URI:** http://j.ustin.co/yWTtmy  
**Tags:** google analytics, google, top posts, top content, display rank, page rank, page views, widget, sidebar, sidebar widget, Google Analytics by Yoast, shortcode, site stats, statistics, stats  
**Author:** Jtsternberg  
**Author URI:** http://dsgnwrks.pro  
**Donate link:** http://j.ustin.co/rYL89n  
**Requires at least:** 3.0  
**Tested up to:** 4.4  
**Stable tag:** trunk	  
**Version:** 1.6.7  
**License:** GPLv2 or later  
**License URI:** http://www.gnu.org/licenses/gpl-2.0.html

Widget and shortcode to display top content according to Google Analytics. ("Google Analytics by Yoast" plugin required)

## Description ##

Adds a widget that allows you to display top pages/posts in your sidebar based on google analytics data.

Requires a Google Analytics account, and the plugin, ["Google Analytics by Yoast"](http://wordpress.org/extend/plugins/google-analytics-dashboard/) (which will be auto-installed by this plugin, thanks to [@jthomasgriffin](http://twitter.com/jthomasgriffin)'s awesome [TGM Plugin Activation Class](http://j.ustin.co/yZPKXw)).

Also includes a shortcode to display the top content in your posts and pages.

### Shortcodes with options supported: ###

* Companion shortcode to widget
`[google_top_content pageviews=5 number=10 showhome=no time=2628000 timeval=2]`  
* Display a post's/page's number of views
`[google_analytics_views]`  
* Conditional text where \*\*count\*\* will be replaced
`[google_analytics_views]This page has received **count** views.[/google_analytics_views]`

### Shortcode attributes definitions: ###

* Pageviews: Show pages with at least __ number of page views
* Number: Number of pages to show in the list
* Showhome: Will remove home page from list: (usually "yoursite.com" is the highest viewed page)
* Time: Selects how far back you would like analytics to pull from. needs to be in seconds. (1 hour - 3600, 1 day - 86400, 1 month - 2628000, 1 year - 31536000).
* Time Value: time=2628000 timeval=2 like in the example above would be 2 months.
* titleremove: Remove site title from listings. (Unless your site doesn't output the site titles, then you will need to add this in order for the filter settings below to work.)
* contentfilter: Limit listings to a particular post-type (post, page, etc)
* catlimit: Limit listings to specific categories. (comma separated category ID's)
* catfilter: Remove listings in specific categories. (comma separated category ID's)
* postfilter: Remove specific posts/pages, etc by ID. (comma separated post ID's)
* thumb_size: Optionally display a thumbnail next to the post title (if the post has a thumbnail)
* thumb_alignment: Thumbnail alignment -- only applies if specifying a thumbnail size

All of the widget options are exactly that.. optional. If you don't include them it will pick some defaults.

### Plugin Features: ###

* Plugin uses WordPress transients to cache the Google results so you're not running the update from Google every time. cache updates every 24 hours.
* Developer Friendly. Many filters built in to allow you to filter the results to dispay how you want.  One example of that would be to remove your Site's title from the results. (now unnecessary, as the widget/shortcode has the option built in)
** [Example using a filter to add view counts after the title](http://wordpress.org/support/topic/top-viewed-content-couple-of-tweeks-needed?replies=9#post-3816989) -

```php
add_filter( 'gtc_pages_filter', 'gtc_add_viewcount_title' );
function gtc_add_viewcount_title( $pages ) {

	if ( !$pages )
		return false;
	// loop through the pages
	foreach ( $pages as $key => $page ) {
		// and add the page count to the title value
		$pages[$key]['children']['value'] = $pages[$key]['children']['value'] . ' ['. $pages[$key]['children']['children']['ga:pageviews'] .' Views]';
	}
	return $pages;
}
```


## Installation ##

1. Upload the `google-analytics-top-posts-widget` directory to the `/wp-content/plugins/` directory.
2. Activate the plugin through the 'Plugins' menu in WordPress.
3. Plugin will prompt you to install the "Google Analytics by Yoast" plugin. Install and activate it.
4. Use the "Google Analytics by Yoast" plugin's settings page to login to your google analytics account.
5. On the widgets page, drag the "Google Analytics Top Posts" widget to the desired sidebar.
6. Update the widget settings and save.

## Frequently Asked Questions ##

### After Upgrading to 1.4, my widget stopped working
I updated the widget options for the date picker, and as a result, it broke any widgets that were saved with the old options. 1.4.1 solves that, but either way, re-saving the widget will correct the issue.

If you were using the shortcode and it broke, you will need to switch to using the shortcode with the new format (described [here](http://wordpress.org/extend/plugins/google-analytics-top-posts-widget/))

### Is it possible to configure the metric being sent to GA, for example to use uniques (ga:uniquePageviews) instead?
* Yes, use this gist: [https://gist.github.com/jtsternberg/918238ff899c2762b41b](https://gist.github.com/jtsternberg/918238ff899c2762b41b)

### Can I display the analytics count next to the title?
* Yes, use this gist: [https://gist.github.com/jtsternberg/449b7ea79fd5ad460143](https://gist.github.com/jtsternberg/449b7ea79fd5ad460143)

### ??
If you run into a problem or have a question, contact me ([contact form](http://j.ustin.co/scbo43) or [@jtsternberg on twitter](http://j.ustin.co/wUfBD3)). I'll add them here.


## Screenshots ##

###1. Widget options.###
![Widget options.](https://github.com/jtsternberg/Google-Analytics-Top-Content-Widget/raw/master/screenshot-1.jpg)


###2. Widget display (in an ordered list).###
![Widget display (in an ordered list).](https://github.com/jtsternberg/Google-Analytics-Top-Content-Widget/raw/master/screenshot-2.jpg)


## Changelog

### 1.6.7
* Fixes "PHP Fatal error: Class 'Yoast_Api_Google_Client' not found" errors when trying to save posts with the shortcode. [Support thread](https://wordpress.org/support/topic/gatcw-plugin-shortcodes-cause-error-500?replies=9#post-7686527).

### 1.6.6
* Use `url_to_postid()` to properly fetch a post ID from a url. [Support thread](https://wordpress.org/support/topic/gatcw-plugin-posts-not-displayed-when-permalinks-do-not-contain-post-slug).

### 1.6.5
* Switch the content filter to a multi-check field, and allow multiple post-type selections. Props [@pmtarantino](https://github.com/pmtarantino), [#9](https://github.com/jtsternberg/Google-Analytics-Top-Content-Widget/pull/9).

### 1.6.4
* Bug fix: Upgrade [TGM-Plugin-Activation](https://github.com/TGMPA/TGM-Plugin-Activation) to fix [an occasional issue](https://github.com/TGMPA/TGM-Plugin-Activation/issues/455#issuecomment-129684199).

### 1.6.3
* Bug fix: "Google Analytics by Yoast" version 5.4.3 changed the name/location of their Google Analytics client class, so need to compensate

### 1.6.2
* Update TGM-Plugin-Activation library.
* Cause shortcode caches to be flushed when the post is updated. 

### 1.6.1
* New filters, 'gtc_analytics_request_params', and "gtc_analytics_{$context}_request_params" for modifying the request arguments to the Google Analytics API. (for things [like this](https://wordpress.org/support/topic/uniques-instead-of-raw-pageviews?replies=1))

### 1.6.0
* Replaced dependency on 'Google Analytics Dashboard' plugin with a dependency on 'Google Analytics by Yoast'
* New filters, 'gtc_list_format' and 'gtc_list_item_format' for modifying the format of the list/list-item output

### 1.5.7
* Update for xss vulnerability, https://make.wordpress.org/plugins/2015/04/20/fixing-add_query_arg-and-remove_query_arg-usage

### 1.5.6
* Feature: Add thumbnail option to widget.

### 1.5.5
* Bug Fix: Fix a few logic issues causing debug.log notices.

### 1.5.4
* Bug Fix: Use a unique transient ID for every shortcode instance.

### 1.5.3
* Bug Fix: `update=true` shortcode parameter (used for busting the cache) did not work properly.

### 1.5.2
* Bug Fix: Fix a couple filters that were getting false-postives.

### 1.5.1
* Bug Fix: Renamed the widget in 1.5.0 which would cause it to be unregistered in any sidebars. Quickly pushed up an update to put it back, but this release makes it final. Apologies for the inconvenience.

### 1.5.0
* Enhancement: New shortcode, `google_analytics_views` for displaying a view count on a single post/page.

### 1.4.8
* Bug fix: Now there is a unique transient for each widget instance.

### 1.4.7
* Improvement: By default won't list duplicate urls with query variable strings (often generated by sharing applications).

### 1.4.6
* Bug fix: Listings wouldn't show when using 'post' as the contentfilter.

### 1.4.5
* Enhancement: More output filters, and check for '?p=' permalinks

### 1.4.4 ###
* Enhancement: Allow html in list item output

### 1.4.3 ###
* Bug fix: Some entities would break the "remove site name" filter.

### 1.4.2 ###
* Fixed the number value select for the "Select how far back you would like analytics to pull from:" selector.

### 1.4.1 ###
* I updated the widget options for the date picker, and as a result, it broke any widgets that were saved with the old options. 1.4.1 solves that, but either way, re-saving the widget will correct the issue.

If you were using the shortcode and it broke, you will need to switch to using the shortcode with the new format (described [here](http://wordpress.org/extend/plugins/google-analytics-top-posts-widget/))

### 1.4 ###
* Added more flexibilty to the time select dropdown. Now with options to select hours and days.

### 1.3 ###
* Added more widget options to modify the list output. Added field to enter repeating elements in the titles to remove from the listings. Also, now limit or filter by post-type, by category, or by post/page ID.

### 1.2 ###
* Increased page-speed with use of transients caching. Also added a few more developer friendly filters.

### 1.1 ###
* Add a pages filter for developers, remove site title from page title, change date picker to use relative dates.

### 1.0 ###
* Launch.
