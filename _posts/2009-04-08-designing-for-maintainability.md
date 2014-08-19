---
title: Designing for Maintainability
author: mnash
excerpt: Designing for Maintainability
layout: post
permalink: /designing-for-maintainability/
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
My recent experiences in open-servo surgery on a Roomba vacuum robot made me think about designing for maintainability. Not in a good way, but more in a bashing-head-against-brick-wall kind of way.

I&#8217;ve found in the past that many things that apply to mechanical devices have their analogs, rough or otherwise, in the software world, so I thought I&#8217;d see where this train of thought might take me.

**Make it easy to open up the thing**  
In the world of machinery, means don&#8217;t use more fasteners than are required for the job, don&#8217;t use 218 different kinds of screws and things to hold on the lid, and don&#8217;t make it so it breaks if you even try to take it apart (and we&#8217;re talking about things that are meant to be fixed and serviced, not things you **want** to explode when opened, which I suppose might be the case in some situations. Generally software isn&#8217;t made to be an IED, although I suppose commercial closed-source software might actually be intended to make it difficult to &#8220;fix&#8221;. Witness the existence of Obfuscators, for example.

In the software world, this means make source code not only available, but accessible and understandable, so you can &#8220;get the lid off&#8221; so to speak, without all the pieces being lost in the process. Perhaps organizing around a standard directory structure, such as the one proposed by Maven, is another item in this pile, as it certainly makes getting rolling with a new project much easier.

**Make it obvious what does what once you do have it open**  
In the machine realm, this reflects good mechanical design, which is generally as simple as possible to get the job done, with no additional pointlessly complex parts and assemblies (as part count being high is generally considered an indicator of lower reliability and maintenance). It&#8217;s not hard to spot machines that were designed to do one thing, then hacked up to do something else, by the existence of pieces that appear to do nothing &#8211; and in fact may really be unnecessary. Many is the time back in my younger days (yes, I can remember back that far) when I&#8217;d put together a motorbike or moped and have parts left over, even though the vehicle ran perfectly well. Of course, this is not a good proof, as my mechanical ability has been suspect for a long time.

In the software realm, this probably is best done via good naming. As an associate said recently, if you name something \*Processor or \*Handler or *Manager, you probably haven&#8217;t thought about it&#8217;s name enough. Ditto for methods/functions &#8211; make their name mean something. Don&#8217;t over-document, especially with tons of comments, as those will probably get out of sync with the software, and can serve more as a distraction than as an aid.

**Good diagnostics**  
Make it easy to tell if you&#8217;ve put it back together correctly. With infernal combustion engines, for example, the engine starting and running serves as a pretty reasonable integration test <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Designing for Maintainability" class="wp-smiley" title="Designing for Maintainability" /> If that doesn&#8217;t work, you go down to unit tests: got fuel? Got air? Got spark? etc.

Ditto with software &#8211; there ought to be at least one good way to tell if what you&#8217;ve done has broken anything (e.g. a high-level smoke test/regression suite), and ways to tell \*what\* you broke if the top-level test conveys bad news.

**Make it easy to put it back together**  
Mechanically, this is closely related to not using dozens of different kinds of fasteners and making stuff require a NASA-level clean room and 14 hands to reassemble &#8216;em.

In software, it means making a clear and flexible build system that isn&#8217;t brittle and dependent on a specific environment. 

Of course, the problem with all these fine observations on designing for maintainability is that the motivation to make something maintainable may not be present in the first place (e.g. as I mentioned about obfuscation). 

Even if the urge to enhance maintainability is there, it may be a very low priority compared to getting working software out the door &#8211; even though we all know that software that lasts for a while is going to spend more time being maintained than it&#8217;s going to spend in initial development. Initial development is urgent, however, and often times the urgent takes priority over the merely important.

I&#8217;m sure there are many other ways to make this analogy, but it surprised me how many jumped to mind after my allergy symptoms subsided once I got the Roomba back together :). 

The patient did not survive the surgery, incidentally. Money for a new one may be sent in lieu of flowers <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Designing for Maintainability" class="wp-smiley" title="Designing for Maintainability" /> 

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