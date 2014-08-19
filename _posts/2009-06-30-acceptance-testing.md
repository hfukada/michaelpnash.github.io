---
title: Acceptance Testing
author: mnash
excerpt: An acceptance test must be comprehensible to the story author, or whatever domain expert is going to actually do the "accepting" that the story has been satisfied.
layout: post
permalink: /acceptance-testing/
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
  - design
  - fitnesse
  - hot deploy
  - integration
  - Java
  - junit
---
Recently I&#8217;ve had the opportunity to consider the right qualities of a tool and/or framework for acceptance testing.

Acceptance tests can be found at a number of different levels, depending on how the story criteria is expressed. (See my previous post on levels of testing) . Often they&#8217;re called &#8220;executable specifications&#8221; if they&#8217;re written in such as way as to describe the behavior of a system in a given scenario.

Often they are functional or integration tests, and generally they are best expressed as &#8220;black box&#8221; tests, that is, tests that have no awareness of the internals of the code or component being tested &#8211; all they see is what goes in and what comes out, and they assert their success or failure based on those elements alone.

An acceptance test must be comprehensible to the story author, or whatever domain expert is going to actually do the &#8220;accepting&#8221; that the story has been satisfied. If they simply take the word of a developer that this big ball of code they see in front of them is testing what they said it should, that&#8217;s not as good as if they can actually read and understand the executable specification (test) themselves. Ideally, they should even be able to author their own acceptance tests, without a developer involved &#8211; perhaps using existing tests as an example.

So, some of the criteria for a good tool might be:

1.  High Visibility: Something that&#8217;s easy to see by all stakeholders
2.  Easily Understood: Something that&#8217;s easy to at least read by any non-developer domain expert
3.  Easily Authored: Something that&#8217;s easy to learn to write
4.  &#8220;Black Box&#8221;: Something that has no knowledge of the internals of the code under test, that only interacts with it from &#8220;outside the box&#8221;
5.  Realistic: Something that tests a version of the application deployed in a realistic environment, as close to production as possible. 

Given these criteria, should the tests be part of the build process for the piece of code under test? For acceptance tests that span modules, this is not practical &#8211; you can&#8217;t actually run the test when you build a module, you can only run it after a certain **set** of modules has been built (and perhaps even deployed).

I would propose that acceptance tests don&#8217;t even belong with the build they&#8217;re testing. I think they belong elsewhere, in an independent location where they can be updated as stories are written and verified. Ideally, there should be a shared space for stories for an entire system or suite of applications, as often a piece of criteria spans multiple components &#8211; so organizing the tests by component is artificial at best.

Another question that comes up when considering tools for these kinds of tests is whether or not they must be stored and versioned with the code they validate. As a developer, my immediate reaction is &#8220;yes&#8221; &#8211; until I think about it a bit. How does it help me to know what tests a **previous** version of my code passed or did not pass? All that tells me is where I was in the past, not where I am now. How much inconvenience am I willing to put up with on the part of test authors to get this capability? Dealing with any version control system is extra work, especially for a domain expert/BA who&#8217;s not also a developer. I&#8217;m now convinced that where I am now is more important than where I was, and being able to easily write and run and make visible tests is more important to me than knowing what happened back in history.

Let&#8217;s examine a few different tools and ways of doing acceptance tests and look at the pros and cons:

**JUnit**  
Developers working with Java have a choice of a number of excellent test frameworks, including TestNG and JUnit. They are likely already familiar with them, and the tests fit nicely into the build cycle of Java applications built with any of the more popular project build and management tools, such as Ant, Buildr, Maven, and so forth.

Our acceptance tests are written just like a functional test, in that they fire up whatever context our application should run within, then provide input to it and verify the output with assertions.

This kind of test is not well-suited for acceptance tests for a number of reasons. First, it&#8217;s hard to separate the code from the test to ensure we&#8217;re truly doing black-box testing. If, for example, we&#8217;re within the same VM as the thing we&#8217;re testing, it&#8217;s very tempting to manipulate objects directly in our test, as opposed to going through, lets say, the publish REST api. This also makes it more difficult to initialize a new testable instance of the application &#8211; to be truly independent from it, our test should spawn a whole new JVM from the system under test &#8211; which is non-trivial from within Java, although of course re-usable fixtures can be written to take the sting out of it.

This doesn&#8217;t help us much when our test spans multiple modules or components, however &#8211; then we must either create stubs for each of the components we depend on, or work in a much more complex deployment process to create a &#8220;live&#8221; version of each of our dependencies.

Finally, a JUnit test is not particularly readable by a non-developer, and not particularly visible, other than as a green or red bar in an IDE or CI server somewhere, so it fails a couple of our most important criteria.

**JBehave, easyb, Specs, RSpec**  
BDD frameworks such as those listed above take our testing power in a different direction. They mostly rely on sophisticated DSL&#8217;s, enabling us to write our tests in a much more english-like fashion, often quite readable to the non-developers who have taken the time to learn a bit of the DSL.

They still suffer from some of the other problems described above, however &#8211; although some of these tools do offer better output formats to make their results more visible (such as the excellent Forms capability in specs, which can show test results in HTML table formats).

They of course still have a learning curve, as the DSLs in each case are another whole language to be learned.

**FitNesse**  
A different approach can be seen in tools like FitNesse, which allows tests to be created in a Wiki, by editing web pages and inserting special markup to call test &#8220;fixtures&#8221;. These fixtures still have to be customized to the situation, of course, but with FitNesse we have the potential of being de-coupled from a single module or system under test, and of developing our tests independently of the code altogether.

The table approach of FitNesse still requires the test author to understand the fixtures available to FitNesse &#8211; this is essentially FitNesse&#8217;s DSL &#8211; but of course only a fairly small number of fixtures need be learned to be able to write a wide variety of tests.

Some projects, however, in an attempt to retain the ability to use FitNesse tests to verify previous versions of their application, take the step of checking the FitNesse tests in to their version control system, thereby losing some of that independence. 

FitNesse has it&#8217;s own ability to track changes to it&#8217;s Wiki pages (and thus it&#8217;s tests), but this is not tied to the checkins or releases of the software under test.

FitNesse makes it easy for a non-developer domain expert to author tests by using existing tests as templates, then changing the inputs to the fixtures being used to create new tests from the existing building blocks. 

These tests and their results are highly visible, especially if the FitNesse wiki is hosted and available to anyone (including developers) to use at any time to verify against a specific deployed instance of the entire suite of applications.

Of course, you&#8217;ve still got the issue of deploying a testable instance of your system to deal with in FitNesse. One approach I&#8217;ve seen to solve this is to actually have a fixture that can deploy the testable instance as part of the set up for the whole test suite, using versions to indicate the revision of code to be tested &#8211; e.g. you have a fixture that says &#8220;deploy module X version 123 to test environment 1&#8243;, &#8220;deploy module Y version 345 to test environment 1&#8243; and so forth, then executes its tests against those deployed instances.

Of course, any database cleanup/reset to get to known state can happen before or just after the deployment, so your tests always start from a known point.

An important part of making this fully automatable is a mutex service: a way to make a call to a known location and say &#8220;check out test environment 1&#8243;, basically saying that test environment 1 is now busy until it&#8217;s released by another call. This ensures that you don&#8217;t start another test run on the same environment while it&#8217;s still in a transition state.

The mutex can also of course report on who has what environment in use, and since when, to detect failures that might not release a lock.

FitNesse has it&#8217;s warts, however, even in a scenario like this, but overall I&#8217;ve seen it succeed more often that other approaches for the high-visibility acceptance tests that many projects need, while tools such as easyb, specs, and RSpec are better for describing behaviours within a single module, and executing as part of that module&#8217;s build process.

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