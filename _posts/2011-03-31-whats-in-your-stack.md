---
title: 'What&#8217;s in your Stack?'
author: mnash
excerpt: "Selecting a set of languages, libraries, frameworks and tools to build your applications with is essential. What's in your Stack? And Why?"
layout: post
permalink: /whats-in-your-stack/
related_exlink_5_desc:
  - 
related_exlink_5:
  - 
related_exlink_4_desc:
  - 
related_exlink_4:
  - 
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
categories:
  - Scala
  - Software Craftsmanship
---
As most of the readers here probably already know, the term &#8220;stack&#8221; when it comes to app development is typically meant to describe the entire software structure on which the application is built. For instance, LAMP is a common example, standing for Linux, Apache, MySQL and PHP.

Developers are often tweaking and re-selecting pieces of their stack &#8211; the newest thing comes along, we like to try it out. But usually we&#8217;ve got a &#8220;go-to&#8221; stack for getting real work done, and constrain our experiments to a separate area until we&#8217;re sure something has what it takes to get included in our favorite stack.

There&#8217;s usually two major types of components in our stack &#8211; the bits we actually deploy, and the bits we use to actually develop with &#8211; the latter includes pieces we usually don&#8217;t actually ship with the finished product.

For instance, a classic J2EE stack might consist of the &#8220;deployable&#8221; pieces: Oracle&#8217;s standard Java EE 6, Hibernate, JSPs (technically a part of J2EE in any case), and Tomcat as a servlet container.

And the development stack might includes Eclipse, Maven, and various plugins to make Maven do our bidding.

There are a number of attributes I wanted in my own personal favored stack. This included:

**Easy management of dependencies:** I like knowing and controlling exactly what bits go into my finished application, and unless I can control all of the dependencies accurately, I can&#8217;t achieve acceptable quality.

**Fast cycle-time:** I want a stack that during development provides me with a rapid cycle time. E.g. the time between making an edit and seeing the results in either an application or test to be as short as possible.

**Easy testability:** I need my stack to facilitate testing, as my normal mode of development is BDD/TDD, where I write code because a tests tells me to, by and large. I want my testing tools to support my choice of test frameworks as well.

**Modern language support:** My choice of language for my own development is [Scala][1], so I need a stack that supports Scala well. I won&#8217;t go into my reasons for choosing Scala, that&#8217;s a topic I&#8217;ve covered [in another blog post.][2]

So, without further delay, here&#8217;s my favored stack. First, the deployable bits:

**Scala:** I&#8217;m currently using Scala 2.8.1. Scala allows me to use a REPL for easy experimentation, which helps with my fast cycle-time requirement as well. The 2.9 release of Scala makes the REPL even more capable, but I haven&#8217;t tinkered with it much yet. I&#8217;ve talked at length about why I choose Scala in other posts, but it&#8217;s not for lack of knowing and having seriously tried other languages and environments. I can&#8217;t say I&#8217;ve tried them all, but I&#8217;ve tried quite a lot, and Scala remains my top choice.

**Scalatra: **[Scalatra][3] is a lightweight non-intrusive web app framework that lets me create web applications quickly, easily, and with maximum flexibility. I can write both RIA-style applications with REST/AJAX/COMET functionality or non-RIA request/response style applications, while maintaining statelessness and supporting scalability.

**Scalate:** With strong integration with Scalatra, [Scalate][4] is a powerful template system, perfect for generating XHTML for web applications in an extremely DRY and expressive manner. It&#8217;s like an up-to-date version of Velocity, but with Scala goodness and much more powerful.

**SBT:** A long-time Maven aficionado, I was hard-pressed to consider a different build system. I was, however, honest about Maven&#8217;s shortcomings, of which there are quite a few. I tried SBT and went back to Maven several times. I was intrigued enough with the advantages to come back again for another try, though, and I&#8217;ve now mastered it enough, and am getting enough benefits, that I won&#8217;t switch back.

**Casbah:**Casbah is the &#8220;missing link&#8221; between the Java MongoDB drivers and Scala. It allows database objects for Mongo to be readily constructed with Scala&#8217;s expressive map syntax, and type-safe retrieval of fields, not to mention it&#8217;s advanced query support.

**Squeryl:** On the occasion I need to interact with relational databases, [Squeryl][5] has become my tool of choice &#8211; but I&#8217;ve also dabbled with a few alternatives. One alternative I won&#8217;t go back to under any circumstances is Hibernate, or even worse, Entity EJB&#8217;s.

**OpenJDK:** Open JDK is a capable and independent JVM that supports Scala well.

**MongoDB:** I&#8217;ve used relational databases for several decades, but now that I&#8217;ve worked with key/value systems such as Mongo, I seldom find a job that RDBMS is better suited for.

**Winstone:** The [Winstone][6] servlet container allows me to create a single simple executable jar that incorporates both my app and the servlet container necessary for it to run in a single super-lightweight package that is easy to deploy and manage. Given it&#8217;s light footprint, it allows me to run multiple servers on a single system and provide a cluster &#8220;in a box&#8221;.

**Linux:** For deployment, I choose Linux. I&#8217;ve never found a business situation that wasn&#8217;t better served by Linux than by Windows, ever. Enough said.

Now the development stack: 

**IntelliJ IDEA:** IDE support for Scala is not fantastic yet, but it&#8217;s quite good and getting better. The best of the lot is IntelliJ IDEA with it&#8217;s Scala plugin. It&#8217;s not perfect, but it&#8217;s quite capable. I will admit I frequently find myself being tempted to use TextMate, Kod, or, more recently, Sublime instead, however, but the completion and refactoring tools keep me sticking with IntelliJ.

**SBT &#038; JRebel:** [SBT][7]&#8216;s own support for continious deployment and testing is excellent, but when combined with the (free for Scala) JRebel tool, it&#8217;s downright unbeatable. I can work on a webapp, make code or UI changes, flip to my browser and hit refresh and see the result. I can tell SBT to keep running my tests every time they need to run, and immediately see any breaks as they occur.

**Jetty:** SBT uses a built-in Jetty servlet to auto-deploy webapps for continuous development, so Jetty is part of my stack as well.

**Mac OSX:** For development, I work on a Mac system much of the time. I do have a desktop Linux system, but the impressive portability and power of my MacBook Air is hard to compete with.

The above are my current weapons of choice for web application development. So, what&#8217;s in YOUR stack, and why?

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

 [1]: scala-lang.org
 [2]: http://php.jglobal.com/blog/?p=1100
 [3]: https://github.com/scalatra/scalatra
 [4]: http://scalate.fusesource.org/
 [5]: http://squeryl.org/
 [6]: http://winstone.sourceforge.net/
 [7]: http://code.google.com/p/simple-build-tool/