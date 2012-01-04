---
layout: post
title: EmailBack.Us - A Need Fulfilled
keywords: back end form email processor static web page
description: A super-simple form to email processor
tags: 
- webdev
- projects
---

<img src="images/emailbackus.png" style="float:left; padding: 5px;"/>
So a few weeks ago, when I was writing the home page for [hugecity.us](http://hugecity.us), I was really excited to be putting together an entire site with no back-end processing whatsoever.  After writing a few Ruby on Rails apps recently it was nice to be able to fit a bunch of separate applications on the same small Rackspace instance.  

I was flummoxed, however, by the contact form.  All my dreams of serving static html, images, and javascript came crashing down when I realized that I'd have to spend **almost an hour** installing and configuring PHP or node.js just to have an emailed contact form.  Not to mention the ever-so-slightly higher processor demands on a box that I planned to stuff to the brim with miniscule experiments.

Surely someone has a service to route data from a web form to my email address, I thought.  A quick google search later, I had found a few.  Unfortunately, the strongest ones looked straight out of the 90s and had a bewildering array of features from custom form builders to required CAPTCHAs and 5 tier pricing schemes.  Nobody had a simple email pipe and nobody's page especially made me want to sign up for their services.  So, I installed php and wrote a script to forward the mail to a HugeCity mailbox.

It did give me an idea for a service that I would find useful:

##EmailBack.us - Real Simple Web Form Processing

I wrote [EmailBack.us](http://emailback.us) over the course of a couple of days using technologies that I was either unfamiliar with or hadn't used in ages.  The entire site is written in PHP using MongoDB as the storage engine.  I hadn't written PHP since about 2005, so it was nice to dust off old skills.  I'd never used MongoDB before, but it seemed like a good, lightweight choice for storing a list of account details and nothing else.  The site has its own postfix running (listening on localhost only, of course) to handle the mail sending without depending on a service provided.  Also learned a bit about DNS SPF records trying to get it all configured properly.

##No passwords!

Everyone hates passwords, especially for site that you seldom visit.  Most people just revert to sending the password reset email for sites they only log into occasionally.  Also, storing passwords (even hashed and encrypted) presents a security risk because most people reuse passwords. 

For a site that's all about email communication, why not just use that medium for logins instead of passwords?  To login, you enter your email address in the signup/login box and you get a link that gives you access for a day!  The link simply contains an access token that expires in 24 hours.  After it expires, nobody can access the account without access to the email.  Might be a problem for enterprise, but I'm targeting small sites and developers who just want a quick form now.

##Monetization?

I wrote this service for myself.  I'm moving HugeCity's form processing over to it and I'm sure I'll use it for the small sites I write in the future for myself and others.  However, if others find it useful and it starts costing me money, I'll probably make some premium updates.  Maybe CAPTCHAs?  Hosted forms in iframes with validations?  Hosted responses instead of emails?  For now, I've fulfilled a personal need and scratched an itch.

