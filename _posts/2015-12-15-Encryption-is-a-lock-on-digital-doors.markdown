---
layout: post
title: Encryption is a lock on digital doors
keywords: encryption security backdoors
description: Why strong encryption is important for every person on the Internet
tags:
- internet
---

Another day, another politician saying that law enforcement needs the ability to define mathematics: [http://www.dailydot.com/politics/carly-fiorina-encryption-backdoors-crypto-wars-2016/](http://www.dailydot.com/politics/carly-fiorina-encryption-backdoors-crypto-wars-2016/)...  not that I'm saying that Fiorina would make a bad president or a bad tech company CEO (she most certainly would and has).  Plenty of other politicians, actually most of them, have made some kind of statement saying that we need TSA locks on every digital door.

There are several problems with this plan:


### Internet locks are not like physical locks

Everybody loves analogies to explain technology, so let's start with that.  Law enforcement rightly has the authority to break locks on doors to access places they have a warrant to access.  The do not, however, have the right to dictate the nature of the door or locking mechanism.  What people are proposing now is just that: dictate the nature of the locks on digital doors. 

This is problematic because of the difference between a digital door and a physical door.  Part of the security of a physical door is its spatial isolation.  A door can be hard to get to.  You have to physically pass through and occupy space around that door to get to it.  For a locked door that you don't have a key for, you have to physically modify (usually break) the door.  

Digital doors have none of these limitations.  You don't have to physically do anything.  Digital doors are not isolated in space.  They exist everywhere at all times.  A better way of thinking about it is like this: 

> Your digital doors open into every other room and space in the world, accessible by criminals and friends alike.

Wouldn't you want the locks on those doors to be as strong as possible?  Would you want to weaken them because the police say "That lock's too strong, we need to be able to access your house in the event of a crime or emergency?"  Of course not, not when *every criminal in the world* is literally waiting right outside of it.
   

### Would you give a spare house key to every police department in the country?

No, of course you wouldn't, because that's insane.  You'd have to place massive amounts of trust in a huge number of people and bureaucracies.  Once violation of trust and security and that key ends up in a criminal's hand.  Except it would be every criminal's hand.  And every criminal is waiting in that room that has every digital door in it.  And that key opens every single door there.


### Math does not work like that

Encryption works because of math.  It works because it takes a long time to compute something without knowledge of a special number.  If you have that special number you can make that computation.  This allows us to ensure that when we ask our bank's website to withdraw $100, they can be sure we are who we say we are, and there is nobody listening to our conversation to gain the knowledge of how to withdraw more money.

What these proposals are talking about is changing that computation so either:

1. You don't have to have that special number if you make the computation a little differently and only the government would know how.
2. You could use a 'master number' like that master locker key the janitor had in High School in lieu of the special number.

Both of these break the trust of the computation.  The first one relies on only the 'good guys' knowing the method.  The second one relies on only the 'good guys' having the master number.  These methods are known as [Security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity).  Secrets never stay secret for long and this would be the world's highest profile secret.  Anybody who had this secret could open any digital lock on the planet.


### Maybe some laws should change

So we have a situation where the only rational design of the system does not allow access to law enforcement servicing a lawfully issued warrant.  This is a problem, I will not disagree with that.  The solution, however, is not to break the fundamental principles of secure digital communications.

With physical doors, an owner of the door would not have to supply a key because a bolt cutter or battering ram could be utilized.  With digital doors it is actually *impossible* to open the door without the number.

The US Constitution protects US citizens from being forced to incriminate themselves.  A lot of people (and courts) have taken this to mean that people can't be forced to unlock digital devices and information because communicating a password or key would be incriminating themselves.  This is not an unrational position to take.

Maybe, though, when a *lawful* court orders someone to open a digital door we should not consider that self-incrimination.  They could always refuse and face contempt of court.  This would have to be done on a case-by-case individual basis, though.  It would have to be done in the open by a judge.  This is the only way I currently see to keep information secure and not completely shut out lawful law enforcement.

I don't know, though, I'm not a lawyer.  That could open up a bigger can of legal worms than I can anticipate.
