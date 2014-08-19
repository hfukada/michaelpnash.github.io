---
title: Levels of Testing
author: mnash
excerpt: 'There are many different levels of test - we explore what they are and when should you use each one.'
layout: post
permalink: /levels-of-testing/
"http://anarchycreek.com/2009/05/20/theyre-called-microtests/":
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
related_exlink_1:
  - 
categories:
  - Software Craftsmanship
tags:
  - functional
  - integration
  - Java
  - junit
  - testing
  - unit
---
I&#8217;ve had reason recently to do some thinking on the various &#8220;levels&#8221; of software testing. I think there&#8217;s a rough hierarchy here, but there&#8217;s some debate about the naming and terminology in some cases. The general principals are pretty well accepted, however, and I&#8217;d like to list them here and expound on what I think each level is all about.

An important concern in each of these levels is to achieve as high a level of automation as possible, along with some mechanism to report to the developers (or other stakeholders, as required) when tests are failing, in a way that doesn&#8217;t require them to go somewhere and look at something. I&#8217;m a big fan of flashing red lights and loud sirens, myself <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Levels of Testing" class="wp-smiley" title="Levels of Testing" /> 

**Unit**  
Unit testing is one of the most common, and yet in many ways, misunderstood levels of test. I&#8217;ve got a separate rant/discussion in the works about TDD (and BDD), but suffice it to say that unit-level testing is a fundamental of test-driven development. 

A unit test should test one class (at most &#8211; perhaps only part of a class). All other dependencies should be either mocked or stubbed out. If you are using Spring to autowire classes into your test, it&#8217;s definitely not a unit test &#8211; it&#8217;s at least an integration test. There should be no databases or external storage involved &#8211; all of those are external and superfluous to a single class that you&#8217;re trying to verify is doing the right thing.

Another reason to write comprehensive unit tests is that it&#8217;s the easiest place to fix a bug: there are fewer moving parts, and when a simple unit tests breaks it should be entirely clear what&#8217;s wrong and what needs to be fixed and how to fix it.

As you go up the stack to more and more complex levels of testing, it becomes harder and harder to tell what broke and how to fix it.

Generally unit tests for any given module are executed as part of every build before a developer checks in code &#8211; sometimes this will also include some functional tests as well, but it&#8217;s generally a bad idea for any higher-level tests to be run before each and every check-in (due to the impact on developer cycle-time). Instead, you let your CI server handle that, often on a scheduled basis.

**Functional**  
Some people suggest that functional and integration are not two separate types, but I&#8217;m separating them here. The key differentiation is that a functional test will likely span a number of classes in a single module, but not involve more than one executable unit. It likely will involve a few classes from within a single classpath space (e.g. from within a single jar or such). In the Java world (or other JVM-hosted languages), this means that a functional test is contained within a single VM instance.

This level might include tests that involve a database layer with an in-memory database, such as hypersonic &#8211; but they don&#8217;t use an \*external\* service, like MySQL &#8211; that would be an integration test, which we explore next.

Generally in a functional test we are not concerned with the low-level sequence of method of function calls, like we might be in a unit test. Instead, we&#8217;re doing more &#8220;black box&#8221; testing at this level, making sure that when we pour in the right inputs we get the right outputs out, and that when we supply invalid input that an appropriate level of error handling occurs, again, all within a single executable chunk.

**Integration**  
As soon as you have a test that requires more than one executable to be running in order to test, it&#8217;s an integration test of some sort. This includes all tests that verify API contracts between REST or SOAP services, for instance, or anything that talks to an out-of-process database (as then you&#8217;re testing the integration between your app and the database server).

Ideally, this level of test should verify \*just\* the integration, not repeat the functionality of the unit tests exhaustively, otherwise they are redundant and not DRY.

In other words, you should be checking that the one service connects to the other, makes valid requests and gets valid responses, not comprehensively testing the content of the request or response &#8211; that&#8217;s what the unit and functional tests are for.

An example of an integration test is one where you fire up a copy of your application with an actual database engine and verify that the operation of your persistence layer is as expected, or where you start the client and server of your REST service and ensure that they exchange messages the way you wanted.

**Acceptance**  
Acceptance tests often take the same form as a functional or integration test, but the author and audience are usually different: in this case an acceptance test should be authored by the story originator (the customer proxy, sometimes a business analyst), and should represent a narrative sequence of exercising various application functionality.

They are again not exhaustive in the way that unit tests attempt to be in that they don&#8217;t necessarily need to exercise all of the code, just the code required to support the narrative defined by a series of stories.

Fitnesse, RSpec and Green Pepper are all tools designed to assist with this kind of testing.

**Concurrency**  
If your application or service is designed to be used by more than one client or user, then it should be tested for concurrency. This is a test that simulates simultaneous concurrent load over a short period of time, and ensures that the replies from the service remain successful under that load.

For a concurrency test, we might verify just that the response contains some valid information, and not an error, as opposed to validating every element of the response as being correct (as this would again be an overlap with other layers of testing, and hence be redundant).

**Performance**  
Performance, not to be confused with load and scalability, is a timing-based test. This is where you load your application (either with concurrent or sequential requests, depending on it&#8217;s intended purpose) with requests, and ensure that the requests receive a response within a specified time frame (often for interactive apps a rule is the &#8220;two second rule&#8221;, as it&#8217;s thought that users will tolerate a delay up to that level).

It&#8217;s important that performance tests be run singly and on an isolated system under a known load, or you will never get consistency from them.

Performance can be measured at various levels, but is most commonly checked at the integration or functional levels.

**Load/Scalability**  
A close relative of, but not identical with concurrency tests are load and/or scalability tests. This is where you (automatically) pound on the app under a simulated user (or client) load, ideally more than it will experience in production, and make sure that it does not break. At this point you&#8217;re not concerned with how slow it goes, only that it doesn&#8217;t break &#8211; e.g. that you \*can\* scale, not that you can scale linearly or on any other performance curve.

**Quality Assurance**  
Many Agile and Lean teams eschew a formal quality assurance group, and the testing such a group does, in favor of the concept of &#8220;built in&#8221; QA. Quality assurance, however, goes far beyond determining if the software perform as expected. I have a detailed post in the works that talks about how else we can measure the quality of the software we produce, as it&#8217;s a topic unto itself.

**Alpha/Beta deployments**  
Not strictly testing at all, the deployment of alpha or beta versions of an application nonetheless relates to testing, even though it is far less formalized and rigorous than mechanized testing. 

This is a good place to collect more subjective measures such as usability and perceived responsiveness.

**Manual Tests**  
The bane of every agile project, manual tests should be avoided like the undying plague, IMO. Even the most obscure user interface has an automated tool for scripting the testing of the actual user experience &#8211; if nothing else, you should be recording any manual tests with such a tool, so that when it&#8217;s done you can &#8220;reply&#8221; the test without further manual interaction. 

At each level of testing here, remember, have confidence in your tests and keep it DRY. Don&#8217;t test the same thing over and over again on purpose, let the natural overlap between the layers catch problems at the appropriate level, and when you find a problem, drive the test for it down as low as possible on this stack &#8211; ideally right back to the unit test level.

If all of your unit test are perfect and passing, you&#8217;d never see a failing test at any of the other levels, theoretically. I&#8217;ve never seen that kind of testing nirvana achieved entirely, but I&#8217;ve seen projects come close &#8211; and those were projects with a defect rate so low it was considered practically unattainable by other teams, yet it was done at a cost that was entirely reasonable.

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