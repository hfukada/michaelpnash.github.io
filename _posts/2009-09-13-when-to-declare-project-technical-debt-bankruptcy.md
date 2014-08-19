---
title: 'When to Declare Project &#8220;Technical Debt Bankruptcy&#8221;'
author: mnash
layout: post
permalink: /when-to-declare-project-technical-debt-bankruptcy/
related_exlink_5:
  - 
related_exlink_4_desc:
  - 
related_exlink_4:
  - 
related_exlink_3_desc:
  - 
related_exlink_3:
  - 
related_exlink_2_desc:
  - 
related_exlink_2:
  - 
related_exlink_1_desc:
  - 
related_exlink_1:
  - 
related_exlink_5_desc:
  - 
categories:
  - Software Craftsmanship
tags:
  - Agile
  - code debt
  - design
  - functional testing
  - technical debt bankruptcy
  - testing
---
We&#8217;re probably all familiar with the term &#8220;technical debt&#8221;, meaning the cost of doing things in a non-optimal or non-quality way. While I can go on at length (as my colleagues can attest!) about how this is avoidable by baking in quality, and thus saving time and money at every turn, the fact is that many existing projects have considerable technical debt.

Setting aside for the moment the discussion of telling &#8220;good&#8221; technical debt from &#8220;bad&#8221; technical debt, let&#8217;s just focus on a projects &#8220;bad&#8221; technical debt. 

If we describe this kind of debt as factors that slow down the ability to change and improve the system, then we see that we are paying the &#8220;interest&#8221; on this debt every time we touch the codebase or it&#8217;s deployed instances. 

What I&#8217;d like to focus on in this posting is the point at which this technical debt is evaluated to be sufficient that it makes sense to do what we&#8217;d normally call a &#8220;re-write&#8221; of the offending system or subsystem. Basically, when the -ah- mud gets so deep that the hip-waders aren&#8217;t helping, it might be time to throw in the towel and start a do-over.

I call this point &#8220;technical debt bankruptcy&#8221;. Much like a real bankruptcy, it&#8217;s an admission that chipping away at the debt isn&#8217;t going to work and isn&#8217;t worth it &#8211; that it&#8217;s time to re-group, and in a chapter-11-ish way, fold our tent in a responsible fashion.

Of course, determining if you&#8217;re at this point is critical. If you&#8217;re not, then you might be throwing out the baby with the bathwater and losing valuable work and former effort for reasons that are not sufficient. Often, political reasons can get us into that kind of situation, where the pressure to do a re-write is not justified. If there are no or few changes to a system, and it&#8217;s working sufficiently well as is, then there may be no reason to declare bankruptcy.

If, however, the bill collectors of technical debt are knocking down the virtual door, it&#8217;s important to know when to make the right move. As the song says &#8220;know when to fold &#8216;em&#8221;.

Part of knowing this is to be able to measure the pace and cost of change, and to be able to estimate, or better, measure, the cost of change if a re-write were done. Let&#8217;s say you&#8217;ve got a legacy project and a new project. The legacy project is using some old technology and techniques that are painful to work with, and you know they&#8217;re causing you to burn more time than they should be. If you also have a newer project (maybe something nice and greenfield) that&#8217;s being done with the latest new and shiny tools, Agile techniques, and so forth, you can get a rough idea of what each feature point in the new project is costing you. Now you can compare this to the cost of a feature point in the old project and make a comparison. 

If you can look at your backlog of epics and get an idea as to what the future cost of maintenance on the legacy project is going to cost you, then you can take this cost and estimate it instead using the ruler of the new technologies and techniques. The delta is the amount you&#8217;ve got available to &#8220;spend&#8221; on a re-write, essentially.

If the math is right, then declare your technical debt bankruptcy and begin anew!

In some further posts, I&#8217;ll explore how to do a well-organized and structured &#8220;chapter 11&#8243; on a project, rather than just dropping the ball, including the part that functional tests play in this process, and look at a re-write as a form of highly aggressive refactoring, rather than a whole new project.

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