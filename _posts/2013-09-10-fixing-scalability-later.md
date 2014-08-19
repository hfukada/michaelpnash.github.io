---
title: Fixing Scalability Later
author: mnash
layout: post
permalink: /fixing-scalability-later/
categories:
  - Software Craftsmanship
tags:
  - parallel
  - reactive
  - scalability
---
There&#8217;s a common wisdom that the right way to build a software product is to build the simplest thing that can work. In the user-facing world, it&#8217;s a bit different, there&#8217;s the concept of a minimum viable product, but that&#8217;s still what you build first.

The understanding most developers have of what that means is that the user-facing features must meet the minimum viable product, but that the back-end should be quick-and-dirty, at least to a degree.

*How* dirty varies, but many developers would agree that concerns such as scalability and performance take a back seat at this point to making the user-facing features work. In some cases developers even skip tests, at least most tests, preferring to build the production code directly.

Niceties such as continuous delivery, scalability and performance are to-do items for the second iteration.

The business driver for this appears at first look to make complete sense: time-to-market is important, and you must get users before your competition gets them.

## False Premises

The problem with this common wisdom is that is often doesn&#8217;t work as well as expected, largely because it&#8217;s based on some false premises.

Here are some of those premises, and what&#8217;s wrong with them:

## Premise: Scalability can be bolted on

While there are *some* things you can do to improve performance once an application is complete and in production, *scalability* is much harder to retrofit. The term scalability doesn&#8217;t mean &#8220;go faster&#8221;. That&#8217;s performance. 

Scalability means your system has the capability to handle significantly larger or smaller load without changing how the software itself works. If you can simply add more machines, more memory, or more threads, that&#8217;s scalable software. If the user load goes down, you take some machines away, without changing anything.

If you have to go change code, especially if you have to change it a lot, that&#8217;s not scalability, or at least it&#8217;s limited scalability.

Often an existing system is built in such a way that it&#8217;s not at all an easy refactor to make it more scalable. For example, a system that relies on server-side page state is very hard to scale, as requests from a specific user must be routed to the same actual server in order to maintain the state. There are horrible &#8220;solutions&#8221; to this problem like sharing the cache of server-side page cache between servers, but they also max out very quickly, and are very complex to boot. Far better is to rely on client-side state, and have the web services themselves stateless &#8211; in this way any one server in the cluster can handle any user&#8217;s request. This is the kind of thing that is *very* difficult to retrofit once it&#8217;s become entrenched.

## Premise: There is such a time as &#8220;Later&#8221;

Every developer knows: There&#8217;s no such time as &#8220;later&#8221;. You don&#8217;t get specific time in this business to add scalability &#8220;later&#8221;. 

What happens in the real world is that you struggle along with your scalability (or other) limitations until they&#8217;re critical, then you do a &#8220;big bang&#8221; process &#8211; either a serious refactor, or a rewrite. Hopefully you&#8217;ve built your system in such a fashion to make that possible in pieces.

This is not an unusual pattern: Many huge names in the business have done exactly this when they hit the scalability limits of their current designs.

## Premise: You don&#8217;t have a scalability problem day one

Scalability works in both directions: It means you can add resources to handle more users, it also means you need less hardware to handle *fewer* users.

Machines and resources equals money. If you&#8217;re hosting on a PaaS, like AWS or Heroku, it&#8217;s quite literally money. If you&#8217;re in-house hosted, you have a &#8220;chunkier&#8221; scale, in the sense that just fully utilizing a machine you already own doesn&#8217;t mean a cost increase, but when you run out of iron it can get very expensive, very quickly.

If you have very few users at first, you want to host them as inexpensively as possible, then just spend more money when and if you need it, not before.

That&#8217;s scalability in both directions.

## Premise: Writing Scalable software is harder than writing non-scalable software

It arguably used to be true that writing software in a way that doesn&#8217;t close any doors for being able to scale was more difficult than writing software without regard to future scalability.

This is in fact the fundamental assertion that makes it worth ignoring scalability: if it costs more time or money to get to market, then you are tempted (quite reasonably) to not do it.

More modern tools and techniques, however, such as reactive programming, undermine this argument. Reactive apps are quite straightforward to build, being virtually the same, code-wise, as their non-reactive and blocking counterparts and arguably easier to test, deploy and maintain, and maintain excellent future potential to scale.

## Don&#8217;t Bolt it On

The goal of deferring scalability until later is to get to market faster, so you can make money.

The snag is that any attempt to bolt on scalability is doomed to waste far more time than if you&#8217;d simply structured for scalability in the first place, so your net profit is much lower.

That&#8217;s on top of the fact that just as your product starts to really surge and succeed, it&#8217;ll die, costing you most of those customers you went to market quickly to get.

If modern techniques make it as easy, or even close, to build scalable apps as to build apps that are hard to scale, why would we built apps any other way?

<div class="g-plusone" data-annotation="inline" data-width="300">
</div>

<!-- Place this tag after the last +1 button tag. -->

  


<div class="st-callout hastitle lightblue center" >
  <h4 class="st-callout-title ">
    Principles and Practices
  </h4>
  
  <div class="inside">
    <i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book: <a href="http://jglobal.com/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="http://jglobal.com/dispatches/">Craftsmanship Dispatches</a> newsletter.
  </div>
</div>

<div class="clear">
</div>