---
title: Feature Conflict
author: mnash
excerpt: Features can conflict with each other as a system grows
layout: post
permalink: /feature-conflict/
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
  - Software Craftsmanship
---
Often, in the software development game, we&#8217;re asked to add a feature to an existing system. Sometimes this system has been around for a long while, as there&#8217;s no notion of &#8220;planned obsolescence&#8221; in much of software.

I recently encountered a situation that is highly symbolic of the problem, if not an actual software issue, per se.

At an office I&#8217;ve worked in, they have very nice washrooms (yes, this is related to software &#8211; bear with me here). They&#8217;re modern, with nice clean stalls and such, and feature toilets with the &#8220;auto-flush&#8221; feature you&#8217;ve no doubt seen elsewhere.

Once you&#8217;ve finished your transaction, you just finish up and leave, and the sensor detects you leaving and auto-flushes the, ah, buffer, for you. Excellent, now you can be free of having to remember to do that yourself, and assured that it&#8217;s already been done when you enter the stall. Kind of like auto-commit on a JDBC connection. Well, kind of.

Anyway, let&#8217;s talk about feature conflict.

A new feature was recently added to this fine setup: paper seat liners. You&#8217;ve probably also seen these &#8211; they&#8217;re the nice little rings of paper in a dispenser, usually on a wall, that allow you to isolate your back-end interface from the implementation details of the toilet seat.

Also very fine idea. In the case of this particular washroom the dispenser for these is attached to the wall behind and above the toilet itself.

Taken independently, each of these features (auto flush and seat liner) seem like perfectly good features, and their implementations are quite reasonable. In functional testing, each performs exactly as it should.

The difficulty comes in integration testing, when you try to use the system as a whole.

Let&#8217;s take a use-case and walk through the scenario: The &#8211; ah &#8211; user enters the system. Standing in front of the toilet, he (definitely he in this particular case) decides to avail himself of the seat liner, and removes an instance from the dispenser. No problem. At this stage, the auto-flush sensor has already detected the presence in it&#8217;s scope, and does nothing, as it doesn&#8217;t trigger until you leave the area.

Now an implementation detail: the way the paper liner works is that the spot in the middle of the paper is cut out, and drops down to touch the water, while remaining attached to the remainder of the liner. The idea here is that when the water leaves during the flush, the liner will be drawn down into the bowl with it, and appropriately de-allocated. As we&#8217;ve said, previous functional tests verify this works just fine.

Now let&#8217;s assume the user has correctly deployed the liner, and wishes to transact his business. Well, if you were facing the toilet when you came in, you probably don&#8217;t want to be anymore at this point, so you turn around. Here&#8217;s where the feature conflict rears it&#8217;s ugly head: the flush sensor, noting the movement, often picks this moment to decide it&#8217;s time to flush.

The liner, having deployed correctly, departs the scene at this point, just as the user completes their interface. Unfortunately, that is the moment at which the liner is supposed to be there. You see (or, more correctly in the case of the user, feel) the problem.

So, which feature is broken? Taken one at a time, neither is broken &#8211; they both do exactly what they&#8217;re supposed to do. The failure is at the point of the wholistic view of the overall system, and neatly demonstrates the fact that it&#8217;s impossible to consider features or potential features in isolation, in any system. You must consider scenarios of users actual interactions with the system, and how the new feature will affect those scenarios.

Nobody said it&#8217;s easy, but it&#8217;s important.

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