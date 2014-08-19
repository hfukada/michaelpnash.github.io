---
title: The Case for the Natural-Language Unbound Variable
author: mnash
layout: post
permalink: /the-case-for-the-natural-language-unbound-variable/
related_exlink_1:
  - 
related_exlink_1_desc:
  - 
related_exlink_2:
  - 
related_exlink_2_desc:
  - 
related_exlink_3:
  - 
related_exlink_3_desc:
  - 
related_exlink_4:
  - 
related_exlink_4_desc:
  - 
related_exlink_5:
  - 
related_exlink_5_desc:
  - 
categories:
  - Humor
  - Tips and Tricks
tags:
  - Tingum
---
I was recounting to a colleague the other day a story that is probably much funnier to fellow developers than anyone else, and thought I&#8217;d share it here as well.

I had the opportunity for a number of years to work with a software team in the Bahamas, for a company with operations there. They were a great group to work with, and we did some good stuff. The Bahamas has it&#8217;s own &#8220;dialect&#8221; of English sometimes, however, and it was a while before I got used to the slight differences and accents from my native Bermudian.

One of my favorite elements of the unique Bahamian dialect is their use of a unbound variable in natural language.

You know when you&#8217;re talking about something, and the name of a specific piece of technology escapes you? Well, those of you with younger memories maybe don&#8217;t have this mental lazy-loading happen quite as often as us old geezers, but I&#8217;m sure it happens once in a while. You&#8217;re saying something about a webapp deployed to a cluster and you want to refer to the device that distributes the processing load of the users across the machines in the cluster. &#8220;Load balancer&#8221; is the term you&#8217;re looking for, but your brain has hit a bad sector and is busy doing an fsck, so you stammer over the right term.

Bahamians have invented a term especially for this situation, and I call it the &#8220;unbound variable&#8221; in natural language. We&#8217;re not sure what it&#8217;s value should be in this situation, but it serves as a place holder when we think of the right word later on. 

It&#8217;s called &#8220;tingum&#8221;, pronounced just like you&#8217;d expect, with a short &#8220;i&#8221;. Its considered bad form to pronounce it &#8220;thing-um&#8221;, I understand, even thought that might be the root of the word originally.

So you can simply say, &#8220;When the tingum moves a session from one server to another&#8221;, rather than having to actually work out the necessary technobabble to go in that spot. 

It saves us the trouble of having to come up with new terms at random, like &#8220;whatsit&#8221;, or the much more verbose &#8220;thing-a-me-bob&#8221; or &#8220;whatchamacallit&#8221;.

It&#8217;s important not to bind this variable to any one term, even if it later becomes clear what that term should be in any one context, because that would reduce it&#8217;s generality. If you **know** that tingum should be bound to &#8220;load balancer&#8221;, you might inadvertently use it in it&#8217;s bound form in the wrong sentence.

In this sense, it&#8217;s rather like &#8220;_&#8221; (the underscore) in Scala &#8211; it&#8217;s \*supposed\* to be unbound.

So, the next time your mental RAM gets a checksum error and you can&#8217;t remember the correct technical term, keep the &#8220;tingum&#8221; in mind!