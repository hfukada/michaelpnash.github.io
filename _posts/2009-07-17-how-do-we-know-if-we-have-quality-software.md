---
title: 'How do we know if we have &#8220;Quality&#8221; software?'
author: mnash
excerpt: What does quality software mean, and how do we know it when we see it?
layout: post
permalink: /how-do-we-know-if-we-have-quality-software/
"http://anarchycreek.com/2009/05/26/how-tdd-and-pairing-increase-production/":
  - How Internal Quality increases Productivity
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
related_exlink_1:
  - 
categories:
  - Software Craftsmanship
tags:
  - code debt
  - components
  - quality
  - testing
---
If you ask most software teams, they&#8217;ll tell you that they would like to be producing high quality software. If you ask them if they are, they might hem and haw, but their answer will depend, more times than not, on subjective criteria &#8211; how they feel about the software their producing.

It&#8217;s important for good software teams to have pride in what they produce, no question, and most developers very much want to produce a quality product, but having the feeling that you&#8217;re producing quality is not enough. We need to actually establish that we **are** producing quality software. But how?

First we have to define what quality software is, as we can&#8217;t say yes or no if we don&#8217;t know what the question means. In this post I&#8217;m going to kick that definition around a bit, then in later posts we&#8217;ll talk about how that definition can be applied to our software to make objective measurements of quality.

Here&#8217;s where we run into our first bit of difficulty, as the definition of quality software is slightly different depending on who you ask. Everyone thinks they know what it is, but it&#8217;s surprisingly difficult to specify when you get asked.

Our best bet then, is to try to determine what the most common attributes of quality software are, the ones that most people would agree are part of a quality software system, or at least would agree have a significant impact on quality. Let&#8217;s list a few, keeping in mind that some of these factors are much more important to some situations that to others. 

**Requirement**  
The best applications as far as quality must be said to begin with high-quality requirements. A topic unto itself, high-quality requirements must be descriptive, not prescriptive &#8211; that is, describe what is required in sufficient detail that it can be clearly understood, yet not say or imply exactly how that functionality is to be implemented, in order to leave the programmer with enough flexibility. A good requirement should also include clear criteria on how to verify if the desired functionality has been achieved &#8211; e.g. a good and consistent definition of &#8220;done&#8221;. There are many more attributes in this area, which we&#8217;ll explore in a future post.

**Quality of design**  
A design that fulfills the requirements and takes into account the other attributes that make up quality is often hard to evaluate. Most developers agree, however, that quality software must start with a quality design. Again, this is a large topic that we&#8217;ll explore in more detail at another time.

**Quality of conformance to the design**  
Something a little easier to quantify is the actual conformance to the design of the system that implements it. Does the code do what the design said it ought to do?

**Reliability**  
Software that continues to operate the same way despite the passage of time and the variation of environment shows the trait of reliability. If the software is deterministic, e.g. it responds the same way to the same inputs every time (unless of course it&#8217;s not supposed to &#8211; like a game with a random element), then it is showing some of the attributes of reliability. If it&#8217;s a service, then it&#8217;s uptime can be used as a gauge of reliability. Reliable software is considered to be of higher quality than unreliable software.

**Maintainability**  
How difficult is it to maintain (e.g. fix and/or improve) the software? Various things about how the software is structured, what language it is written in, how it&#8217;s modularized, and many other factors can help give us an idea as to the software&#8217;s maintainability. Easier maintainability is a widely accepted attribute of quality software.

**Completeness**  
Quality software is complete: it not only implements every part of the design, it includes the necessary pieces the allow it to stand either without a lot of supporting systems, or at least with a small well-defined set of such systems. Software that stops short of the complete design can&#8217;t be said to have this aspect of quality.

**Verbosity**  
The verbosity, or rather the lack of it (e.g. the terseness) of the actual source code can be a contributing factor to quality, at the correct level. Too terse and we can have obscure and unreadable source, too verbose and we&#8217;ve got the same. Where the sweet spot is depends a lot on the programming language being used, but it&#8217;s often an aspect of quality that directly affects readability and maintainability.

**Portability**  
Although not an attribute in some cases as far as portability from one environment to another, it&#8217;s generally considered a good thing if software is not overy dependent on it&#8217;s environment &#8211; and this is also an indicator of portability. Higher quality software will be able to be used in a variety of different environments more easily than lower quality software.

**Consistency**  
An overall consistency of both design and implementation is certainly related to quality &#8211; if we have three pages in our UI design, for instance, they should share some common attributes.

**Testability/verifiability**  
The ability to test software is a critical quality metric. If it&#8217;s easy to test, it&#8217;s almost certainly of higher quality than if it&#8217;s hard to test. Software that can be verified as correct is even better, although somewhat rare and generally requiring a functional programming environment.

**Usability**  
Usability is an aspect of quality that is often the hardest to quantify, although certainly not impossible. It doesn&#8217;t only refer to software that&#8217;s intended to have a user-facing portion, but may actually apply to software designed as a web service or utility &#8211; the usability in this case is more a function of how easily other systems and programs can connect to it and consume it&#8217;s services.

**Efficiency**  
Although related to performance to some degree, quality in efficiency is more concerned with making the best user of what resources are available, rather than the overall speed of processing. You might measure aspects of efficiency by looking at memory footprint, CPU utilization, and so forth. A higher degree of efficiency would usually translate into a lower percentage consumed of the available resources.

**Security**  
Although the requirement for this type of quality can vary, it is generally true that software that takes into account security and is by default secure is considered of higher quality than software that is insecure. Witness OSV and Windows, for example (donning flame-proof suit) <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile How do we know if we have Quality software?" class="wp-smiley" title="How do we know if we have Quality software?" /> 

**Coupling**  
An aspect of quality closely related to usability in many cases is the degree of coupling, sometimes also called the degree of dependance. If a software application or service requires a lot of other services in order to do it&#8217;s job, it often is exhibiting a lower quality in terms of coupling compared to a system that has few dependencies, as the system with more dependencies can be harder to install, deploy and maintain. In a SOA environment, of course, a service can reasonably expect to depend on other services, but as few as possible is generally best. 

How the coupling is handled in terms of packaging and distribution can also be an important quality aspect.

**Composability**  
This aspect is best demonstrated by the traditional Unix command-line utilities, such as grep, sed, pwd, and so forth. They do one thing, and do it simply but well &#8211; but they are eminently composable, being designed to be strung together to handle more complex tasks. If a service or application exhibits high composability, it is easily able to be fit into a series or of such services to perform more complex tasks than any one of them can handle alone. 

A high-quality component is often one that can stand alone and perform a useful task, but also be combined with other packages as required easily and quickly.

Ensuring that all of the criteria (or at least all the ones we care about in our situation) usually requires a certain level of quality and consistency to our process, as well, but that&#8217;s another whole discussion.

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