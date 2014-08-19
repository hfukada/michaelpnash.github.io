---
title: Technical Debt Bankruptcy
author: mnash
excerpt: |
  Technical debt tends to increase the cost (in time, a.k.a money) to add each new feature or change to your system. Over time, this cost climbs, usually not steadily or regularly, but in an inexorable path that makes each new change a bit harder than it should be. Often this leads to taking shortcuts, applying the "broken windows" logic that if there's already a mess in the code, what's a bit more mess?
layout: post
permalink: /technical-debt-bankruptcy/
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
tags:
  - code debt
  - functional
  - technical debt
  - testing
---
## How to manage &#8220;Chapter 11&#8243;

&#8220;Chapter 11&#8243; is my slightly tongue-in-cheek term for the time in a project just after you declare technical debt &#8220;bankruptcy&#8221; and decide to do something about it.

### Going Bankrupt

Technical debt is that inevitable accumulation of items in your codebase that could be better. They slow you down, and often end up on a list somewhere as something to fix when you get around too it. Round tuits being in short supply, they often stay on that list for a long, long time.

Technical debt tends to increase the cost (in time, a.k.a money) to add each new feature or change to your system. Over time, this cost climbs, usually not steadily or regularly, but in an inexorable path that makes each new change a bit harder than it should be. Often this leads to taking shortcuts, applying the &#8220;broken windows&#8221; logic that if there&#8217;s already a mess in the code, what&#8217;s a bit more mess?

It&#8217;s often very subtle: you don&#8217;t realize you&#8217;re getting that much slower on every feature request, and you don&#8217;t realize you&#8217;re avoiding doing some features because the code in the area you need to change is &#8220;scary&#8221;, but it happens.

### Point of no returns

In this context, I&#8217;m defining technical debt bankruptcy as the point where the value derived from adding new features or changes to an existing system exceeds the *lifetime* value of those features. 

For instance, you&#8217;ve got this customer invoicing system that has devolved into a steaming morass, and you need to make a change to make it easier to send dunning letters, let&#8217;s say. The change, because of the mess, will cost you $10,000. You expect the system to be in production for another five years before it&#8217;s replaced, and you&#8217;re going to save $1,000 a year by adding the feature compared to typing up the letters manually. In this case, it&#8217;s nice and clear-cut: get a typewriter, you&#8217;re better off.

Unfortunately, in the real world it&#8217;s seldom that obvious: it&#8217;s hard to say what the cost of the change is until after you&#8217;ve done it, as estimating gets harder and harder in a messy system. You&#8217;ve generally got no real idea what a feature will save (or earn) you, and you probably don&#8217;t know how long the system will continue to be used. The only safe thing to do is to keep technical debt to a manageable minimum, so you can proceed without needing a crystal ball. This often doesn&#8217;t happen.

What this adds up to is that it&#8217;s not that clear when you&#8217;ve crossed the point of diminishing returns until you&#8217;re **way** past that point, and it&#8217;s painfully obvious.

When it *does* become clear you&#8217;ve passed that point of diminishing returns, what are the options?

### Paying up

Essentially there are two choices in most cases: Rewrite the system in question, or clean it up so it doesn&#8217;t cost a fortune to make every change. There&#8217;s less of a difference between these two than it might seem.

Here&#8217;s where the decision gets even harder: There are serious disadvantages in rewriting a system, especially if it takes a while and the old one is still in motion, with some changes still getting pushed through &#8212; you&#8217;re chasing a moving target. If you re-write with the same developers that made the mess in the new place, you&#8217;ll probably just have a shiny new mess, as bad as the old one, in the end.

Of course, once the replacement is in place we reap the benefits, assuming we build the new stuff with all of the proper techniques and eye to quality that we did not (presumably) do with the old one &#8211; otherwise we&#8217;ve just doomed ourselves to repeat history, and doubled our cost in the process.

No, let&#8217;s assume we know what we&#8217;re doing with the new system, and that it will be done the &#8220;right way&#8221;. How do we find time and resources to get the new system off the ground?

This is sometimes described as replacing the wings on the airplane while it&#8217;s still in flight. How do you do that? Very, very carefully <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Technical Debt Bankruptcy" class="wp-smiley" title="Technical Debt Bankruptcy" /> 

Another approach is to simply build a new airplane, fly it up alongside the old one, and transfer the passengers from one to the other. This is where we construct our new system and migrate the users and data from one to the other in an organized fashion. The disruption to the passengers is definitely greater than in the first case (where they may not even notice the new stuff happening), but it may be overall safer, as we&#8217;re not disconnecting bits from the old airplane mid-flight at all.

In both cases, a key factor is measuring the functionality of the existing system.

You can&#8217;t replace a thing unless you can measure a thing, and tell what it&#8217;s currently doing. Each feature must be sufficiently well understood to be able to say if it&#8217;s functionality can be adequately replaced by the new system, and it&#8217;s value must be understood to determine if it&#8217;s even necessary to replace it: maybe it&#8217;s better to just remove that feature, not implementing it in the new system.

Often in older systems you will find features that aren&#8217;t being used at all, and haven&#8217;t been in years. It would be a waste of developer dollars to replace these, but **proving** that they&#8217;re indeed not being used can sometimes be difficult. You can&#8217;t guess, you must measure.

For other features, it&#8217;s easy to see what they **look** like they&#8217;re doing, or even what they were intended to do. It&#8217;s not uncommon, though, for those features to be used in a way that was not originally foreseen, so don&#8217;t make assumptions. Measure &#8211; in this case, by communicating with users and ask them about the tasks they use features to perform, to derive a true business value. Then you can write a proper use case to re-build the feature in the new system with confidence.

So, if you&#8217;ve determine via a set of decoupled functional tests exactly what your existing system does, how do you go about injecting this re-write into your Agile process? 

You might be tempted to write stories to replace each feature &#8211; e.g. &#8220;re-implement feature X&#8221;. In my opinion, this is a mistake, on several levels.

Firstly, it means that the replacement must be prioritized by your customer proxy and planned into a sprint (if you Scrum, or gotten into your backlog if you Kanban). The problem is that technical debt is not easily visible at the business level, so it will tend to be prioritized at &#8220;negative infinity&#8221; (as a colleague put it so succinctly), e.g. it&#8217;ll never get to be important enough to get done &#8211; therefore you go on pouring money into the black hole of the existing system.

Secondly, if we&#8217;re defining a new feature as a replacement, exact or otherwise, of an existing feature, then it has, by definition, no direct business value. You already **have** a feature to do that operation, you can&#8217;t (and won&#8217;t) justify another one that does the exact same thing. You can&#8217;t even write a story for it in the classic &#8220;as a&#8230; I want&#8230; so that&#8221; format, which is also a smell.

No, I&#8217;d consider this type of replacement of a feature, even if it&#8217;s a real re-write, as a **refactor**. This means it&#8217;s not a separate story, it&#8217;s handled as a part of a &#8220;real&#8221; story. 

Let&#8217;s look at this scenario: You want to replace feature X with a new version. The next time any story touches feature X, you &#8220;build in&#8221; the time and effort required to re-write feature X into the estimate. Let&#8217;s say story Y was to add a new doohickie to feature X, and would cost 5 dev-bucks (whatever that is &#8211; some arbitrary unit of cost), assuming it&#8217;s applied to the existing feature X (not it&#8217;s rewritten replacement). If story Y is applied to the **new** feature X, it would only cost 2 dev-bucks. To replace feature X (without story Y) will cost 10 dev-bucks. Now you&#8217;ve got a delta of 5 dev-bucks compared to just doing story Y on the existing feature X, but for only 5 dev-bucks more, you get the new feature X, then for another 2, you get story Y.

You estimate 12 dev-bucks to do story Y, and the first sub-task in story Y is &#8220;re-write feature X&#8221;. This assumes you&#8217;ve already got functional tests around feature X &#8211; if you don&#8217;t, then you need to build that cost in as well.

Ouch, you say? Well, yes, there&#8217;s some expense here for sure. The good news is that the **next** time you touch feature X, you start to go the other way &#8211; it takes way less time to make your change than if you hadn&#8217;t spent the 12 dev-bucks now.

Now, this is, of course, to state the blindingly obvious, not as easy as it sounds. <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Technical Debt Bankruptcy" class="wp-smiley" title="Technical Debt Bankruptcy" /> We&#8217;re assuming here that you **can** re-write feature X in isolation, or that you can even test it in isolation from your functional tests. This is where a system designed for modularity and easy testing is really handy, and those are not two attributes of many legacy systems. You may be required to a a fair bit of refactoring just to decouple your existing features sufficiently to get to this point.

Nobody said declaring technical debt bankruptcy was easy or fun, after all, but in some cases it may be the responsible and professional thing to do.

The hard work starts when you consider how to recover, whether it&#8217;s a clean re-write, or a hybrid refactor as we describe here.

<div class="st-callout hastitle lightblue center" >
  <h4 class="st-callout-title ">
    Want to take your craft further?
  </h4>
  
  <div class="inside">
    <i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book (almost finished!): <a href="http://jglobal.com/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="http://jglobal.com/dispatches/">Craftsmanship Dispatches</a> newsletter.
  </div>
</div>

<div class="clear">
</div>