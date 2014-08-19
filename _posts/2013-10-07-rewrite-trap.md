---
title: The Rewrite Trap
author: mnash
excerpt: "Software developers often consider a rewrite when problems with an existing application accumulate. This is usually the wrong approach, and I've seen many projects fail when trying it. Here we discuss the problems and an alternative."
layout: post
permalink: /rewrite-trap/
categories:
  - Software Craftsmanship
tags:
  - code debt
  - components
  - design
  - technical debt
  - testing
---
There is a trap out there in the software business, and I&#8217;ve seen so many teams fall into it that I thought I&#8217;d write down a few thoughts in case it saves some team somewhere from the pain.

Software developers, particular good ones, like to be proud of their creations. That&#8217;s a good thing, and pride in workmanship is to be encouraged. Often, however, we end up with a system or software product that we are less than proud of. That doesn&#8217;t always mean that someone else wrote it, of course &#8211; I&#8217;ve written plenty of software I&#8217;m not proud of, I&#8217;m sure you have too. It does mean, however, that we&#8217;re driven to try to fix it, if we possibly can.

Nothing wrong with that either: but the next move is the one where the trap lives. We often hear the refrain &#8220;the existing system is (fill in many derogatory details), the only way to fix it is to start from scratch with a new system&#8221;.

Although it seems quite reasonable at first consideration, it turns out that in practice, this statement is almost always wrong, and following through on it usually ends badly.

Let&#8217;s consider why, and what superior alternatives might exist, if any.

### Technical Debt

Ward Cunningham&#8217;s metaphor of technical debt is helpful in explaining what happens to some legacy systems. Over time, developers who are under the mistaken belief that time to market is more important than quality and code cleanliness build pieces of code that are harder to read, test, and change than they need to be. Everytime someone tries to change this code, or add to it, they spend more effort and more time than they should have to, generally exceeding the &#8220;time saved&#8221; in writing it in a mess in the first place very quickly, sometimes on the first change. 

At the same time, if the code is already a mess, the &#8220;broken windows&#8221; principle tempts the next developer to leave it a mess, or even add to the mess with more mess, making the problem rapidly worse.

There are many reasons why this happens, the prime amongst them being developers that simply don&#8217;t know any better. Sorry if that seems blunt, but it&#8217;s quite true: not only is it the inexperienced developer who makes the problem in the first place, they are usually the ones that are blind to the problem, as they really have no means to discriminate between good code and bad code, between good design and catastrophies waiting to happen.

When this technical debt builds to the point where every new feature or change is costing more than it&#8217;s lifetime revenue potential, you&#8217;ve hit a point where the suggestion of a re-write is usually made.

### Rewriting a major system is almost always a mistake

Even if the existing code is a horrible mess, a full-on re-write from scratch is seldom a good idea, for many reasons that we enumerate below, plus I&#8217;m sure a few I&#8217;ve missed.

### Never catching up

One problem that is usually present to a degree is the fact that the team responsible for the re-write must &#8220;catch up&#8221; in terms of functionality with the existing system before you can think about migrating users. In a full rewrite, this means the entire functionality of the existing product must be reproduced, plus the affect of any improvements or changes made while that re-write is happening. If you&#8217;re lucky enough to have a system that hardly changes, you might be able to put off the problem entirely, so it&#8217;s likely that you&#8217;re re-writing a system that *does* change, with either new features or bug fixes you must adopt into the new system.

If you&#8217;re building the new system with the same developers as made the mess in the first place, there is little reason to hope the new system will be much better, and the probability of catching up is even less, as all changes to the old system must be duplicated in the new, so the re-write team must be moving a whole lot faster than the maintenance team.

### Disrupting users

Even if you do catch up, or catch up close enough, there is little chance that the new system will be exactly like the old one. The temptation to fix some of the problems with the old system is likely going to cause you to build in some of those fixes during the re-write, so when you release the new system, your users are in for a jolt, no matter how smooth the transition is.

The only alternative is to keep *both* systems around for a longish while, perhaps only using the new system for new users &#8211; this is a sure-fire way to bleed your company and your team dry.

### The Migration Migraine

If you do decide to cut all users over to the new system, you&#8217;re usually faced with the challenge of how to do this, as there&#8217;s no doubt some data in the old system that the users will want in the new ones, and I&#8217;m betting the data formats or schemas on the new one *aren&#8217;t* the same as the old one.

Often this work isn&#8217;t budgeted for properly, and is rushed, causing users to be further disrupted, possibly leaving your product for some other product, defeating the cost savings you were hoping to get by re-writing in the first place.

### Losing Knowledge

No matter how much of a mess an existing system is, it&#8217;s usually more or less operational, and often has been for a long time. During it&#8217;s lifetime it has no doubt seen many bug fixes, many changes, many edits, no matter how hard these were.

All these changes and fixes represent a large pool of knowledge built in to the old system. It may not be obvious, or at all easy to extract, but it&#8217;s there.

Subtle changes that were requested by users, or little fixes that got made to the scheme that one saturday morning that fixed that annoying intermittent performance issue &#8211; they&#8217;re all baked in to your old system somewhere, and they&#8217;re all gone when you replace it wholesale.

This can make the &#8220;lurch&#8221; of the cut-over even worse, and cause further revenue erosion.

### The Alternative

If the road of a re-write is fraught with peril, then what&#8217;s the alternative? If the mess is so bad we can&#8217;t just keep burying it any more, what&#8217;s a development organization to do?

Fortunately, there is a path, and often a hard but good one, that doesn&#8217;t disrupt either your developers or your customers anywhere near as much. It takes work, though, and it takes *strong* technical leadership, with management backing all the way, to make it happen.

You need a small (two or three at the very most) group of experienced developers to help guide the existing team out of the swamp of their own making, and often they won&#8217;t like it, as developers defend knowledge they already have much more than you might expect. That&#8217;s where the backing of management comes in, to set expectations and limits so the process doesn&#8217;t devolve into endless debate.

The nutshell of the alternative approach is to decompose and re-organize the existing system, turning it into small enough pieces that *can* be either rewritten or significantly refactored until the technical debt is down to a manageable and appropriate level.

### Decompose

The first, and perhaps hardest, part of the alternative approach to a big re-write is to *decompose* a single large application into smaller more manageable pieces.  
Re-writing components/services

### Evolving the UI

Almost in every case I&#8217;ve seen it, one of the greatest impediments to decomposing an existing application that has accumulated a lot of debt is that the user interface of that app is tightly coupled with the rest of the product. In some cases, the UI code *is* the whole app, and contains everything from the UI layer down to the persistence layer, all wrapped into a gordian knot in what should have been just the presentation layer.

Untangling that knot is hard, but it&#8217;s *not* impossible, no pun intended. It&#8217;s usually a matter of deriving the true business domain, then teasing apart the UI layer from the controller, the services or other components, and the persistence. Sometimes this also involves starting to break the framework addiction, by creating layered classes that are your own interfaces which can then be implemented by the framework, instead of referring to the framework-supplied classes directly.

In the middle of it, this can look like a worse mess than what you started with, but that&#8217;s not true: as the layers separate, it becomes easier to test, easier to change, and easier to work on, all symptoms of a codebase that is getting healthier, even if it appears more verbose even while it still does the same functions as it did before you started.

### A Digestable Elephant

As is often said, the only right way to eat an elephant is one bite at a time.

The real trick is to find the right seams to decompose the system, and to decouple enough of the right places to make rapid and seemingly radical changes without incurring the wrath of the many problems of a side-by-side rewrite.

Often it helps to use a completely different tech stack and language for the new pieces, just to make a &#8220;clean break&#8221; with the old code and it&#8217;s mechanisms, as otherwise it&#8217;s too easy to slide back down in the quicksand of the old approaches. Often, this is an advantage, as many messy systems have been built with older technical stacks that don&#8217;t lend themselves as well to aggressive refactoring and componentization, or to the ability to be tested and changed easily. The most common symptom of this is &#8220;framework addiction&#8221; where the old system can&#8217;t be disentangled from the framework it was built from.

Overall, I&#8217;ve seen the approach of decompose used far less often than the big-bang re-write, but I&#8217;ve seen the decompose method work every time, as opposed to the big-bang re-write method, which I&#8217;ve only seen really successfully applied in about three cases, and those were where the product involved was not very large or sophisticated, where it was more like replacing a single module in a larger system.

Have you seen the re-write trap sprung on your team? Drop me a line in the comments! 

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