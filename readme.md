[![Build Status](https://travis-ci.org/pfefferle/wordpress-webmention.svg?branch=master)](https://travis-ci.org/pfefferle/wordpress-webmention) [![Issue Count](https://codeclimate.com/github/pfefferle/wordpress-webmention/badges/issue_count.svg)](https://codeclimate.com/github/pfefferle/wordpress-webmention) 

# Webmention #
**Contributors:** pfefferle, dshanske  
**Donate link:** http://14101978.de  
**Tags:** webmention, pingback, trackback, linkback, indieweb  
**Requires at least:** 4.7  
**Tested up to:** 4.7.3  
**Stable tag:** 3.1.1  
**License:** MIT  
**License URI:** http://opensource.org/licenses/MIT  

Webmention for WordPress!

## Description ##

[Webmention](http://www.w3.org/TR/webmention/) is a web standard that enables conversations across the web, a powerful building block that is used for a growing federated network of comments, likes, reposts, and other rich interactions across the decentralized social web.

When you link to a website, you can send it a Webmention to notify it. If it supports Webmentions, then that website may display your post as a comment, like, or other response, and presto, you’re having a conversation from one site to another! 

## Frequently Asked Questions ##

### What are Webmentions? ###

[Webmention](http://www.w3.org/TR/webmention/) is a simple way to automatically notify any URL when you link to it on your site. From the receivers perpective, it's a way to request notification when other sites link to it.

### That Sounds Like a Pingback or a Trackback ###

Webmention is an update/replacement for Pingback or Trackback. Unlike the older protocols, the
specification is recommended by the W3C as well as an active community of individuals using
it on their sites.

### How can I send and receive Webmentions? ###

On the Settings --> Discussion Page in WordPress:
* Activate sending Webmentions by checking the "Attempt to notify any blogs linked to from the article" option
* Activate receiving Webmentions by checking the "Allow link notifications from other blogs (pingbacks and trackbacks) on new articles" option.

You can use the `send_webmention($source, $target)` function and pass a source and a target or you can fire an action like `do_action('send_webmention', $source, $target)`.

[vimeo https://vimeo.com/85217592]
-- Video by [Andy Sylvester](http://andysylvester.com/2014/01/27/working-with-webmention-video/)

### How do I support Webmentions for my custom post type? ###

When declaring your custom post type, add post type support for webmentions by either including it in your register_post_type entry or adding it later using add_post_type_support. This
will also add support for receiving pingbacks and trackbacks as WordPress cannot currently distinguish between different linkback types.

### How can I handle Webmentions to my Homepage or Archive Pages? ###

Webmentions should be allowed on all URLs of a blog. The plugin currently supports only Webmentions on
posts or pages, but it is very simple to add support for other types like homepages or archive pages.
The easiest way is to provide some kind of a default post/page to show collect all mentions that are no
comments on a post or a page. The plugin provides a simple filter for that:

    function handle_exotic_webmentions($id, $target) {
      // do nothing if id is set
      if ($id) {
        return $id;
      }

      // return "default" id if plugin can't find a post/page
      return 9247;
    }
    add_filter("webmention_post_id", "handle_exotic_webmentions", 10, 2);

## Other Notes ##

### Caching ###

The URL for the webmention endpoint, which you can view in the source of your pages, should be excluded from any server or plugin caching. 

## Changelog ##

Project and support maintained on github at [pfefferle/wordpress-webmention](https://github.com/pfefferle/wordpress-webmention).

### 3.1.2 ###
* Enable option for page support
* Allow custom post types to declare support for webmentions as a feature which will enable pings.

### 3.1.1 ###

* URLEncode/Decode source and target
* Webmention Comment Type now declares support for avatars
* Meta keys are now registered for `webmention_target_url` and `webmention_target_fragment`
* Target URL is stored instead of derived from the permalink to ensure permanance
* Target fragment is stored to support fragmentions. Can also suport comments when reply is to a comment.

### 3.1.0 ###

* added page support (server and client)
* moved `webmention_post_id` filter to a global function (thanks @dshanske)
* fixed https://wordpress.org/support/topic/form-for-entering-manual-pings-stays-on/
* fixed some typos

### 3.0.1 ###

* Show endpoint discovery on every page again, to prevent several problems.

### 3.0.0 ###

* Plugin refactored to use API infrastructure.
* Visiting the endpoint in a web browser now returns a webmention form.
* Plugin now compliant with draft specification although remains synchronous.
* Deprecation of webmention_title and webmention_content filters in favor of a single targeted webmention comment data filter.
* webmention_post_send action now fires on all attempts to send a webmention instead of only successful ones. Allows for logging functions to be added.
* Supports adding additional parameters when sending webmentions
* Fix incompatibility with Ultimate Category Excluder plugin.

### 2.6.0 ###

* removed duplicate request for HTML via get_meta_tags
* refactoring
* limits to same domain

### 2.5.0 ###

* add salmon/crossposting-extension support (props @singpolyma)
* disable self-pings via settings
* do not unapprove already-approved webmention (props @singpolyma)
* some code improvements

### 2.4.0 ###

* switched to WordPress Coding Standard

### 2.3.4 ###

* some fixes and improvements

### 2.3.3 ###

* added filter for webmention endpoint (to add/require additional paramaters: <https://github.com/pfefferle/wordpress-webmention/issues/39> or <https://github.com/pfefferle/wordpress-webmention/pull/41>)

### 2.3.2 ###

* added more params to `webmention_post_send` (props to @snarfed)
* removed rescedule of webmentions (props to @snarfed)

### 2.3.1 ###

* use error-code 403 instead of 500 if pingbacks/webmentions are disabled for a post (thanks @snarfed)
* added `webmention_comment_parent` filter

### 2.3.0 ###

* nicer `title` and `content` discovery
* added post-id to `webmention_links` filter
* improved `publish_post_hook` function
* disabled flood control
* nicer response value
* some more filters/actions
* added a default request "action" to be more flexible and to handle more than mentions on posts and pages
* a lot of small fixes

### 2.2.0 ###

* prevent selfpings
* added support for https and http
* optimized some methods

### 2.1.4 ###

* fixed pseudo hook

### 2.1.3 ###

* fixed some warnings

### 2.1.2 ###

* now ready to use in a bundle

### 2.1.1 ###

* nicer feedback for the Webmention endpoint

### 2.1.0 ###

* nicer `title` and `content` discovery
* added post-id to `webmention_links` filter
* improved `publish_post_hook` function

### 2.0.1 ###

* small fixes
* nicer excerpt extractor

### 2.0.0 ###

initial release

## Installation ##

1. Upload the `webmention`-folder to the `/wp-content/plugins/` directory
2. Activate the plugin through the *Plugins* menu in WordPress
3. ...and that's it :)

## Upgrade Notice ##

### 3.0.0 ###

This update brings the plugin into compliance with the draft standard. As a result, some filters and
actions have changed. Please check any dependent code before updating.

### 2.0.0 ###

This plugin doesn't support the microformts stuff mentioned in the IndieWebCamp Wiki.
To enable semantic linkbacks you have to use <https://github.com/pfefferle/wordpress-semantic-linkbacks>
