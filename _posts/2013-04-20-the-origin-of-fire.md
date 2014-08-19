---
title: 'The Origin of Fire: Monitoring and CQRS'
author: mnash
excerpt: How Monitoring and CQRS helped my team detect a problem before anyone else noticed and fix it before anyone else was bothered.
layout: post
permalink: /the-origin-of-fire/
categories:
  - Software Craftsmanship
tags:
  - CQRS
  - Monitoring
---
My team had the chance to deal with a few fires today, and how we went about it got me thinking (and writing, apparently).

It matters quite a bit how you find out about problems, it seems. Perhaps this is obvious in retrospect, but today definitely highlighted it.

For instance, we had a bug on one of our deployed applications that wasn&#8217;t noticed on any of our test environments, and affected our production servers only. No-one noticed it outside the team, we simply saw an error in our email, and a line on a graph showing that something hadn&#8217;t gone quite right, so we dove in and worked on it. This particular one was a tough nut to crack, but we kept at it and got it fixed in a couple of hours &#8211; often we fix things much quicker.

At the same time, our monitors showed a problem with a lack of disk space on another (test) server, so we got some help from another team and had that one sorted out pretty quickly, although it certainly complicated our lives a bit.

Then we found a count we checked against another source for another urgent project seemed wrong, so we spawned a task to check that out&#8230;.

<p style="text-align: left;">
  <a href="http://50.116.19.42/wordpress/wp-content/uploads/2013/04/Fire_Extinguisher-e1366427820749.png"><img class="size-full wp-image-1584 alignleft" alt="Fire Extinguisher e1366427820749 The Origin of Fire: Monitoring and CQRS" src="http://jglobal.com/wp-content/uploads/2013/04/Fire_Extinguisher-e1366427820749.png" width="200" height="284" title="The Origin of Fire: Monitoring and CQRS" /></a>All in all, a day of mostly fire-fighting.
</p>

At then end of the day, the cybernetic gods smiled on us and we got everything back in good er, and before five o&#8217;clock, so we all left feeling pretty positive.

Thinking back on the day, I realized that none of the problems today were discovered *outside our own team*. Although we made a point of mentioning to other teams that we had a problem, as it might affect work they were doing, no-one outside the team *detected* the problems.

Thinking back on it, I&#8217;m pretty proud of that. It indicates two things, I believe &#8211; first, that when something starts to go wrong, we&#8217;ve got a pretty good monitoring system. Secondly, when something goes wrong the harm is contained to a very small portion of our system.

For the first, we make extensive use of a number of monitoring tools, in this case it was <a href="https://www.icinga.org/" target="_new">Icinga</a> that first notified us of the problem, then we immediately turned to our graphs produced in near-real-time by <a href="http://graphite.wikidot.com/" target="_new">Graphite</a> to see the source of the problem. Once we identified the flow problem, we used [Graylog][1] to get the detailed traces we needed to fully locate the issue.

So, that was the fire alarm. Why didn&#8217;t the fire spread?

Our entire system is organized around an Event-Driven architecture, with many small deployable units. We [separate our write processes from our read models][2], so even if a write process goes down (which in this case it did), the read model is still fully available, and was in fact in constant use. The read model, if you do it right, it usually considerably simpler than the write process, so it&#8217;s easier to ensure it keeps going.

Where do your fires start, or at least, from what source do you come to notice them?

If it&#8217;s your own monitoring, that&#8217;s pretty good. If something emails you and says &#8220;fix this, right here&#8221;, you win compared to if your customer calls and says &#8220;something strange just happened&#8230;. somewhere&#8221;, or if another team notices the issue before you do.

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

 [1]: http://graylog2.org/
 [2]: http://martinfowler.com/bliki/CQRS.html