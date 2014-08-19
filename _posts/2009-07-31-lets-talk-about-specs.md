---
title: Lets talk about Specs
author: mnash
layout: post
permalink: /lets-talk-about-specs/
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
  - Scala
tags:
  - BDD
  - Java
  - junit
  - Scala
  - specs
  - tdd
  - testing
---
I project I happened across a while ago is starting to intrigue me more and more: [Specs][1]

It&#8217;s a framework written in [Scala][2] designed to support Behavior-Driven design and testing. This style of testing encourages tests to describe the be &#8220;behavior&#8221; of the class or component under test, ideally in way that is easy to understand by both developers and non-developers alike.

How does this differ from other forms of testing? Mostly in the way functionality is described &#8211; a feature is expressed in terms of a series of interactions with the system under test, describing functionally in a narrative form. We don&#8217;t describe a functional technically, as in &#8220;passing 43 should result in a response of &#8216;ABC&#8217;&#8221;, but in terms of valuable feature interactions, such as &#8220;when a valid login is entered, the foo link becomes available to be clicked&#8221;, for example.

Behaviour-driven design and development make sure we&#8217;re developing code that implements the right features, as opposed to test-driven development, which focuses more on developing the code correctly and accurately. BDD and BDT is more about the &#8220;what&#8221; as opposed to the &#8220;how&#8221;, in other words.

If the subject-area expert for the system under development can understand the language of the test, then it becomes more of an executable specification than just a test &#8211; it may even form the acceptance criteria for a story or feature, especially when multiple such specifications are chained into a narrative.

Flowing from the oft-described &#8220;As a&#8230; I want&#8230; So that&#8230;&#8221; way of describing a story, a narrative describes a sequence of flow through an application, describing and verifying the behavior of the system at each step in the narrative.

Specs supports this very nicely, allowing you to write in a DSL (Domain-Specific Language) which is nonetheless a fully capable programming language at the same time (in this case, Scala).

The basic unit of a Specs test is the &#8220;specification&#8221;, implying, appropriately, that you literally write executable specifications &#8211; documentation that actually verifies that it properly describes the system being described!

Scala is, by design, an extremely extensible language, so it&#8217;s support for DSL&#8217;s such as specs is very good &#8211; it doesn&#8217;t burden you with a lot of unnecessary syntax or verbosity, so the resulting specification is highly readable and relatively english-like. So much so that it&#8217;s even possible for a domain expert non-developer to write, much less read, the executable specifications &#8211; especially if they have examples to go from.

Scala fits seamlessly into any JVM-based environment, plays nicely with IDEs, Ant, Junit, Maven, and all the tools you might already be using to build your systems, so it&#8217;s adoption doesn&#8217;t cause much of a ripple effect. Scala files simply live in a directory structure inside an otherwise all-Java project, for instance, and are compiled to .class files, just like Java.

Specs also leverages other powerful test frameworks, such as Mockito, JMock and Scalacheck, among several others.

My team is using Specs in two modes, so far: One is as a part of the primary build process, just like you&#8217;d run your JUnit or SpecsTest tests. The Scala tests in this case are used as either actual unit tests (although expressed in a behavior-driven way) or in-process functional tests (if they include several classes or a whole subsystem under test).

The other way we use Specs is as a set of stand-alone acceptance tests. In this mode we run Specs externally from the system under test. This is especially useful for our systems that rely heavily on REST web services. In these cases we write our narratives to assert various responses from the REST services found at various URLs, while launching Specs from Ant in it&#8217;s own VM on another box entirely. These are true &#8220;black box&#8221; tests, where the tests have no knowledge of or access to the code under test &#8211; they must interact with the running system in a very &#8220;real world&#8221; way. This provides an ideal environment for acceptance tests, especially given the readability of the Specs specificiations. Our user-proxies also like the fact that the test itself can&#8217;t be influencing the code &#8220;inside the box&#8221;, as it&#8217;s easy for programmers to write &#8220;happy path&#8221; tests <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Lets talk about Specs" class="wp-smiley" title="Lets talk about Specs" /> 

Of course, once you&#8217;ve used specs and Scala for your testing, you may be tempted to infiltrate it into your other development, but that&#8217;s another post <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Lets talk about Specs" class="wp-smiley" title="Lets talk about Specs" />

 [1]: http://code.google.com/p/specs/
 [2]: www.scala-lang.org