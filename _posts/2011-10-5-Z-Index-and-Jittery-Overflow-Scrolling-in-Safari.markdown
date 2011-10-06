---
layout: post
title: Z-Index and Jittery Overflow Scrolling in Safari
keywords: css scroll overflow safari rendering tearing jittery jump
description: Solution to div scrolling tearing/jumping in Safari
tags: 
- webdev
- techtips
---

Here's a little tech tip I just learned.  I can usually find solutions to problems like this from a quick google search, but couldn't find anything about this.  Hopefully this will be indexed and the next person will not waste as much time as me:

I just wasted almost an hour debugging some CSS in Safari with a funky scrolling issue.  I have an absolutely positioned div that I want to be scrollable.  I'm also using some drop shadows to set off the list from a background on one side.  So, like a moron, I started messing around with z-indexing.  Here's what my scrolling div looked like:

{% highlight css %}
.list_container {
	position: absolute;
	left: 70px;
	top: 90px;
	bottom: 0;
	right: 0;
	overflow-y: auto;
	z-index: 2;
}
{% endhighlight %}

I had a couple of elements I wanted to look "behind" the scrolling div, so I just upped the z-indexing.  Looked fine in FF and Chrome, but scrolling in Safari had terrible artifacts.  The entire pane would tear, and all the elements in the parent container would jump up and down with the scroll events.  The effects got worse the slower the rendering (zooming the page made it awful).  I was a bit confused because it looked like a rendering engine issue, but it worked fine in Chrome (also webkit).

Now, as I tried to fix it I didn't know it was a z-indexing issue and only got to the actual problem through desperate isolation of EVERY css attribue of the scroll pane and its container.  I just removed the z-index from the **.list_container** class and adjusted the other classes accordingly.

So, word of warning: 
> Don't assign z-indexes to divs that you want to use overflow on if you care about the page working correctly in Safari.  