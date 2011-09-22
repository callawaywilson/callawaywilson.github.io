---
layout: post
title: Thinking of AJAX Requests as a Secure Web Service
---

It's VERY easy to unintentionally create security holes using the asynchronous features of modern web browsers. Time was when the only holes in a web server were the HTTP request for a file and the occasional CGI script. Now, ajax requests can outnumber the normal page requests by a significant margin.  We don't always consider that these request are coming from the client space.

One of my co-founders (hugecity.us) was working on a feature to share events via email and his initial design basically set us up as an open relay for any signed in user (well, you'd have to understand the ajax request, but that's kind of the point). The message and headers were composed in javascript on the browser.  If we can off-load processing to the client, why not?  The rails controller took in the mail attributes as parameters (to address, reply-to address & message body). Now it didn't literally relay, because it was always coming from our email address, but they could send any message content to anyone from our email address. Ouch.

He's a very security-minded admin and developer, so of course he caught it before it was even close to deployment, but it illustrates an issue that gets way past the design phase and into live code far too often. When writing code to run in the browser you must assume that it is not necessarily the code that will be run by the client. You are essentially "suggesting" a set of client-side interaction and hoping that they will just run it as you give it to them, because it's hopefully much easier for them to use your implementation.

So how can we prevent these kinds of security errors from slipping through? Well, I think that by conceptualizing the browser a little differently we can save lots of money and hairlines:

> The Browser is a Web Service Client!

...and your in-browser client code is a reference implementation of the client. While there are unsecure web services out there, they are in general a lot more secure than callback endpoints for ajax requests. This is because a web service developer sees the web service as the security line. You never trust any inputs from the clients (this true for pretty much everything).

So, when designing an interactive web site that you want callbacks for, design your web services (no quotes, because that's exactly what they are) first. Treat your browser code as a client, composing your web services into something useful. If you have a team divided between front-end and back-end, this will also improve developer relations, as the two teams will be able to speak through an API instead of this random feature or requirement.