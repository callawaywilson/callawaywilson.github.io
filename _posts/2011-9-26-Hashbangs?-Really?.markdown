---
layout: post
title: Hashbangs? Really?  Here's a functional alternative
keywords: hashbangs html5 history browser compatibilty url
description: A good cross-browser way to treat URLs properly with History.pushState()
tags: 
- webdev
- techtips
---

So yeah, twitter does it.  If twitter started putting up unskippable flash ads, would you put them on your site?  No? Of course not, because it's a bad idea. URLs are supposed to represent an actual resource on the server that you're asking for, even for your fancy one-page site. Yes it's impossible to make HTML5 URLs work universally (seriously IE, still?), but that doesn't mean that we need to break URLs for well behaved browsers.

At [Hugecity.us](http://hugecity.us), we all of our content without page reloads.  It's all based around a google map, so we don't want to load everything again just because people want to look at a new event.  Of course, we want each event to have a unique and well-formed URL.  Essentially our site is one page with many URLs.  We looked into and rejected using hashbangs universally because real URLs look better and facebook sharing requires a real URL to get opengraph metadata.  So, we needed to actually serve the data by real URL.

We use a wonderful javascript tool called history.js by Benjamin Arthur Lupton (on [github](http://github.com)).  It provides a simple API that wraps HTML pushState() for supporting browsers and hashes for browsers that don't play nice.  Of course, this does fragment the URLs between the different browsers, which can be a big problem if you want people sharing and forwarding links to your site.  We just have to make sure that the URLs can play nice with each other: Hashed URLs should change to normal URLs in supporting browsers and normal URLs should change to hashed URLs in non-supporting browsers.

## Hashing Strategy

First, we need to determine a scheme for our URLS.  I think it works best if you just design your resource URLs as if they weren't going to be hashed.  And then put a hash in front of the entire thing if you need the hash.  This works best on a one-page app like twitter or hugecity.  For example, **http://awesomeco.com/awesomecontent** becomes **http://awesomeco.com/#awesomecontent**.

Next, we need to decide how we'll serve our content.  At hugecity, we have a base web application served at the root and a JSON-based API to fetch the actual content.  For the web urls, if you fetch content, that resource is inlined in the page served.  For example, if you request **http://hugecity.us/**, you'll get something like this:

	<scripts/>	
	<html templates/>

But if you fetched **http://hugecity.us/event/1794/Braves_v_Phillies**, you'd get

	<eventdata/>
	<scripts/>	
	<html templates/>
	
Of course, if you request **http://hugecity.us/#event/1794/Braves_v_Phillies**, you won't get the eventdata, so we need to figure out how to glue them together:

## Supporting Hashed URLs in HTML5 browsers

So a user with an HTML5 browser comes in on a hashed URL they found: awesomeco.com/#awesomecontent, but the content is really at awesomeco.com/awesomecontent. Simply put in a javascript redirect:

{% highlight javascript %}
if (!History.emulated.pushState && window.location.hash.length > 1) {
  window.location = '/' + window.location.hash.substring(1, window.location.hash.length);
}
{% endhighlight %}

This will detect if the browser supports HTML history but is looking at a hashed URL and change the browser's location to the proper one.

## Supporting Hashed URLs in non-HTML5 browsers

If someone comes in with that same hashed link, and the browser doesn't support HTML pushState, then all we need to do is detect the hashed data and asynchronously fetch the content they really requested.

{% highlight javascript %}
if (History.emulated.pushState && window.location.hash.length > 1) {
  var resource = parseResource(window.location.hash);
  handleContent(API.fetch(resource));
}
{% endhighlight %}

## Supporting normal URLs in non-HTML5 browsers

The last special case that needs to be handled is a non-hashed URL being requested from a non-HTML5 browser.  Since we can only change the content after the hash, we need to redirect the browser to the root and put a hash in front of the resource that they requested, then we can emulate the pushState with History.js.

{% highlight javascript %}
if (History.emulated.pushState && window.location.pathname.length > 1) {
  window.location = '/#' + window.location.pathname;
}
{% endhighlight %}

Now it works via the method in *Supporting Hashed URLs in non-HTML5 browsers*

So there you go, pushState in browsers that support it, hashes in browsers that don't support pushState, and the links are completely portable between the two.  And when your last user using hashes vanished to the dust bin of history, your site will work correctly.