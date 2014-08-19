---
title: Why Modularity?
author: mnash
excerpt: Why is modularity in our software systems a good thing?
layout: post
permalink: /why-modularity/
related_exlink_1_desc:
  - 
related_exlink_1:
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
  - API
  - components
  - design
  - Java
  - JVM
  - Maven
  - Modularity
  - Module
  - OSGi
  - testing
---
![modularity Why Modularity?][1]

I&#8217;ve been sold for some time on the benefits of highly modular software development (and deployment, for that matter, almost equally importantly).

However, I&#8217;m aware that not everyone is on the same page, or has the same definition of &#8220;modularity&#8221; in the first place, so I thought I&#8217;d collect and enumerate the things that have convinced me, as best I can.

I&#8217;ve been in the software business for a very long time, and sometimes I have a preference or leaning towards a certain technique or technology. Sometimes that preference has clear causes behind it, but sometimes not. Modularity is one of the latter, where I **know** it&#8217;s not only good, but critically important, but it&#8217;s hard for me to immediately say why or how I know that in a succinct way.

So, I apologize for the length of this explanation, as I&#8217;ve not yet taken the time to make it shorter <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Why Modularity?" class="wp-smiley" title="Why Modularity?" /> 

**Modularity Defined**  
First things first: What do I mean by modularity? 

In short, I mean a system comprised of relatively small self-contained units. The idea of modularity has caught on much more completely in many other disciplines, but far less so in software. In manufacturing, especially mechanical and electronic, in business, especially finance, the idea of modularity is well established. Modularity is used to increase and maintain quality, and reduce cost while increasing output. In the automotive industry, for example, extensive use of standardization and modularity allows us all to afford a car, as opposed to just the wealthy or the mechanically inclined. 

In the software world, the use of modularity is still woefully small, however. When it is employed, though, some spectacular successes have arisen. One of the oldest examples is Unix, arguably the most successful operating system ever. Since 1969, the &#8220;do one thing, do it well, and play well with others&#8221; modular design of Unix has been the basis of it&#8217;s success and flexibility, allowing it to span everything from embedded devices to mainframes.

The Java Virtual Machine (JVM) is another realm where modularity is on the rise, and starting to have an impact. Many different approaches are available, and some of them work with any of the large number of languages available on this platform.

**Increase overall success rate of projects**  
In the many software projects I&#8217;ve been involved with over the years, I&#8217;ve noticed a few trends. Smaller, well-contained projects have a higher success rate than larger and more poorly contained projects. (By contained, I mean the number of places and ways the project interacts with other projects is small). I&#8217;m sure there are a host of reasons for this, but part of it is simple comprehension &#8211; small projects are generally easier to understand than big one, so the number of times things get done wrong is reduced.

A system comprised of well-isolated modules tends to be more like a set of small projects that happen to work together, so I find this reason alone a plus for modularity.

But this hides much of the detailed reasoning behind why modularization works, so let&#8217;s dig a bit deeper&#8230;

**Makes the API between components explicit, not hidden**  
Sometimes I heard the argument that modularity is complex, that it actually increases the difficulty of working with a system. I find that doesn&#8217;t hold up under examination: when modularity seems complex, it&#8217;s probably because it&#8217;s being done wrong, or being retrofitted to a system that was not designed with modularity in mind. What you&#8217;re really seeing in this situation is that the attempt to modularize is **exposing** the complexity that was already there.

When a system is properly designed in a modular fashion, the APIs between modules are small and well-defined, with a limited number of cross-module dependencies.

**Reduce unnecessary complexity**  
By reducing a large complex system into a series of small and better understood modules, we&#8217;ve reduced the complexity we have to deal with at any one time. This means that the overall large system only has to deal with how the exposed APIs of our modules will be fitted together, treating the modules themselves as &#8220;black boxes&#8221; that perform specific functions, without worrying about how they perform it.

In both cases, we&#8217;ve reduced the complexity we need to deal with.

I specify here &#8220;unnecessary&#8221; complexity, as of course the complexity of the issue itself doesn&#8217;t get any simpler just because we modularize it &#8211; but if we don&#8217;t have to deal with a lot of tangled plumbing, we can concentrate on the real issue.

**Increase testability**  
A module that performs a single function is much easier to test exhaustively than an entire monolithic system. The number of interdependence is limited, meaning we can do more of our testing at the unit and orchestration level than at the functional or integration level, meaning our feedback time is improved and our coverage likely increased.

This means our development velocity can increase, as the impact of changes can be evaluated more easily and more quickly.

![modtank swimwall 05 Why Modularity?][2]  
**Support Composition**  
When you have a number of smaller building blocks, it&#8217;s relatively easy to reshuffle those blocks to change the behaviour and functionality of your overall system. This is making use of composition &#8211; connecting blocks together to do more than they can on their own, and its a pattern that is supported well in a modular environment. 

Although composition is often thought of in the context of re-usable modules, when building a new system, it&#8217;s also valuable in modules that are only used within one system, as it allows the large-grained behavior of the system to change much more rapidly than without modules.

Composition makes large complex systems easy to understand and work on, and vastly increase the maintainability of the overall system.

**Impact of changes isolated**  
The isolation of changes to an effected module is a major benefit of modularity, especially as it supports maintainability. If you&#8217;re constantly concerned with your changes affecting parts of the system you&#8217;re not actually working on, you&#8217;re not able to go as fast as you could if you knew that your changes would only apply to a small area of the whole system &#8211; the current module. 

This is related to and similar to the support for refactoring that unit tests give &#8211; if you&#8217;re tests are all green after your refactor, you know you haven&#8217;t changed the functionality of your system. In modularity, if you&#8217;re isolated from other modules in the system, this goes a step further &#8211; you can change the functionality of the module freely without concern about other bits of your system breaking. This is true if you&#8217;re doing anything that&#8217;s not in the one package you&#8217;ve &#8220;exported&#8221; as the service definition.

**Allows physical design to reflect logical design**  
Modularity also allows developers to build systems where the logical design actually corresponds as needed to the physical design, an often overlooked abstraction. Kirk&#8217;s <a href="http://techdistrict.kirkk.com/2009/01/07/jar-design-over-class-design/" target="_new">blog post on the topic</a> describes this issue better than I could, so I refer you there.

![fischertechnik building blocks Why Modularity?][3]  
**Supports Refactoring Better**  
Refactoring is the process of changing the implementation of a system without changing it&#8217;s behavior. One of the primary reasons to write unit tests, for instance, is to support and allow refactoring, so we know the system does the same thing when we&#8217;re done as when we started.

Modularization supports this ability by making clear the portions of a system that affect other modules, and the portions which do not. When you&#8217;re refactoring in a monolithic system, even with IDE support, the scope of your changes is the entire project. When you&#8217;re refactoring in a modularized system, if you&#8217;re &#8220;inside&#8221; the module, you have no need to consider scope on the outside, as there isn&#8217;t any. And when you&#8217;re refactoring the exported interfaces, you know ahead of time your scope is cross module, and can take it into account.

In short, modularization lets you refactor more freely within a module, and lets you be intentional and organized when refactoring between modules.

A colleague recently suggested that modularization would interfere with the ability to see a system as a whole. It&#8217;s been my experience that the exact opposite is true &#8211; a well structured set of modules can still be considered as a whole when necessary (an aggregator POM is any easy way to set this up in the Maven universe), but it also allows modules to be worked on &#8220;safely&#8221; in isolation, which a monolithic system does not. This ability to only look at one piece at a time is all the more critical the larger the system becomes.

The need to refactor &#8220;across&#8221; modules is a warning sign, in my opinion &#8211; it generally indicates that the API between modules is changing, and this is a change you want to be more aware of then any amount of changes within modules. If it happens often, it probably indicates that the module boundaries are not yet stabilized, and you have more design work to do.

![advanced blocksjpeg Why Modularity?][4]  
**Scalable Development**  
A modular system lends itself well to many hands being involved in it&#8217;s development and maintenance. It&#8217;s not necessary for a team or a pair to understand the whole system well, or even at all &#8211; they can still work on a small well-defined and decoupled module, and can do it in parallel with development on other modules.

**Helps prevent Design Rot**  
As discussed in <a href="http://techdistrict.kirkk.com/2007/10/08/rotting-design/" target="_new">this blog post</a>, design tends to degrade over time, especially in large monolithic systems. Modularity helps to prevent this rot, as pieces that become superseded by better ways of doing things can be replaced individually, and the impact to the overall system managed and isolated. This is akin to removing a brick from the wall and replacing it with a better brick, rather than tearing down the wall.

**Solves the classpath hell problem entirely**  
Classpath hell is the name for the condition where a large number of dependencies are &#8220;in scope&#8221; at once. It&#8217;s not unique to Java, or even the JVM. It is apparently called &#8220;DLL hell&#8221; on Windows environments, but I&#8217;m happy to report I know very little about that. I do know it can happen on platforms other than the JVM, however.

By isolating the influence of dependencies, modularization, especially the way OSGi does it, makes it an explicit process to import and export exactly what packages you wish to and from your modules. What the module uses in it&#8217;s private implementation under the hood is no longer relevant to the system at large.

What happens in the bundle **stays** in the bundle, in other words, with appropriate apologies to Las Vegas. <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Why Modularity?" class="wp-smiley" title="Why Modularity?" /> 

Management of dependencies is the cure for classpath hell, and modularization is key to this, as described in [this excellent article][5].

![image 04 Why Modularity?][6]  
**Allows smaller pieces of the system to be versioned**  
A key element in continuous releasability is the careful versioning of both individual modules and their dependency requirements. Modules give you the ability to release pieces of your system, not the whole system, better supporting the idea of continuous releasability and enhancing maintainability.

An [article about software maintenance][7] that a colleague recently sent me describes the problem perfectly &#8211; and independently versioned modules is a large part of the answer to this problem.

**Re-Use**  
Although re-use it touted often as a major benefit of modularity, I&#8217;d categorize it as the **least** important benefit, not the most. Although the idea of re-using well-designed modules in new projects is indeed very powerful, it&#8217;s beyond the technical and design capabilities of many teams, often causing them to reject the need for modularity because they see no reason to build for re-use. 

In a way, they&#8217;re right: you **don&#8217;t** build for re-use. You build for just the specific case at hand, but when you separate concerns properly and adhere to modularity best practices, you end up with a module that may lend itself to later re-use much more easily. If such a re-use case emerges, well and good, then you can reap the benefit. It is a lot like a framework &#8211; you can&#8217;t design a good one in isolation from it&#8217;s use cases &#8211; a framework is an emergent artifact from the re-use of code on many different (although similar) projects. The same is true of re-usable modules: you don&#8217;t set out to build a module explicitly to be re-usable.

Allows dependencies to be isolated: e.g. all Weblogic-specific code in one module, or all XMLMill-specific code in one module, increasing ability to refactor safely

Suggested Reading:  
[Agile Architecture Requires Modularity][8]  
[Modularity Patterns][9]  
[Runtime and Development time Modularity][10]

In a later post we&#8217;ll look at some of the counter-arguments against modularity, and why I think they&#8217;re not especially valid or convincing in my experience.

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

 [1]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/modularity.jpg "Why Modularity?"
 [2]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/modtank_swimwall_05.jpg "Why Modularity?"
 [3]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/fischertechnik_building_blocks.jpg "Why Modularity?"
 [4]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/advanced_blocksjpeg.jpg "Why Modularity?"
 [5]: http://techdistrict.kirkk.com/2009/04/06/software-rot-manage-those-dependencies/
 [6]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/image-04.png "Why Modularity?"
 [7]: http://cacm.acm.org/magazines/2009/11/48444-you-dont-know-jack-about-software-maintenance/fulltext
 [8]: http://techdistrict.kirkk.com/2009/06/15/agile-architecture-requires-modularity/
 [9]: http://techdistrict.kirkk.com/2009/08/05/modularity-patterns/
 [10]: http://techdistrict.kirkk.com/2009/06/23/the-two-faces-of-modularity-osgi/