---
layout: post
title: Social Counts Two Night Project
keywords: counts social personal project
description: Announcing Social Counts, a quick way to gauge a url's popularity on the web
tags: 
- webdev
- projects
- counts
---

Announcing Social Counts\: [counts.callawaywilson.com](http://counts.callawaywilson.com)

I recently was doing some work to try to calculate the "popularity" of things online.  One of the methods I tried was counting the number of times the url for the event had been shared on online services.  I ran across a few sites and gems that do that kind of thing: [sharedcount.com](http://sharedcount.com) by Yahel Carmon and this gem: [github.com/vitobotta/share_counts](https://github.com/vitobotta/share_counts).  

I didn't end up using the data, but thought the idea might make a good quick project.  I started learning Ruby on Rails earlier this year to implement [hugecity.us](http://hugecity.us) but hadn't really exercised on a small app yet.  So from "rails new socialcounts" to rebuilding my server on rackspace (I managed to remove yum accidentally and figured I wanted to redo everything anyways...) I had my app in < 10 hours of actual work, including coding, design, and server setup.

What's running right now is just the start of what I'd like to do.  It's easy to expand the supported sharing sites, so I'd like to add some more.  I'd like to count twitter hash tags, products, scan codes, and other kinds of resources.

So, I just thought I'd share a couple of cool things that I learned:

## Using markdown as a view template in Rails 3

All the functionality on the site is just a form a list of counts, but there is some content and documentation.  I really didn't want to format the content as HTML or event HAML.  The README and this post were written in [Markdown](http://daringfireball.net/projects/markdown/), and I thought that it would make sense to just not repeat myself.  After checking out a few markdown gems, I couldn't find anything that would act as a template handler so I could just put the .markdown file in the views.  I didn't want to put in some kind of CMS system for 10K of static text, so I wrote a quick Markdownizer template handler with syntax highlight support:

{% highlight ruby %}
class MarkdownHandler < ActionView::Template::Handler
	def call(template)
		Markdownizer.markdown(Markdownizer.coderay(template.source)).inspect
	end
end

#Register Handler
ActionView::Template.register_template_handler(:md, MarkdownHandler.new)
{% endhighlight %}

This will render the template (without any variables or ruby code) through the Markdownizer coderay and markdown renderers.  Stick it in an initializer at "config/initializers" and you can put markdown in .md suffixed files in your view.  Huzzah!

## Non-production rails environments are lazy about loading classes

The way I had implemented the share counting logic betrayed my Java roots.  I created a generic 'Share' class that held most of the logic for invoking, parsing, and interpreting the various APIs that I'd be talking to.  I then subclassed it to include the differing logic and values of each endpoint.  I suppose modules to support JSON APIs / HTML scraping would have made sense too...  Anyways, I wanted to have a class method in 'Share' collect all of its subclasses, fork out a fetch, and the join the results.  I found a great way to do this:

{% highlight ruby %}
ObjectSpace.each_object(Class).select { |klass| klass < self }
{% endhighlight %}

Except that I always got back an empty set. Turns out that non-production rails environments don't load all the code at startup, but at every request.  That's is awesome while you're testing, but it make reflection tasks like this impossible to run.  Since I don't want my production code to be different from my development, I just ended up enumerating all the classes.  Oh well.
