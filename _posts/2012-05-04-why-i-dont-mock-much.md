---
title: 'Why I don&#8217;t Mock much'
author: mnash
layout: post
permalink: /why-i-dont-mock-much/
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
  - Software Craftsmanship
---
I promised some time back to provide to some of my team members parts the background material I use to reason my way to my current aversion to mocking, and the reason I prefer stubs over mocks for testing applications.

It turned out this was a longer road than I had anticipated, but reviewing my reasoning was helpful, so I&#8217;m finally providing some of the reading material related to it here, as well as my own conclusions for consideration.

First, it&#8217;s good to understand the differences between stubs and mocks (and other kinds of test fakes). Martin Fowler explains this quite precisely <a target="_new" href="http://martinfowler.com/articles/mocksArentStubs.html">in this article.</a>

Sub-call verification (e.g. orchestration testing) is an anti pattern and impedes refactoring. Mocks use behaviour verification at a low level, and encouraging testing it.

Another description of the difference, with a slightly different take is <a target="_new" href="http://blog.callistaenterprise.se/2010/11/12/stubs-n-mocks/"> in this article.</a>

Another analysis of the difference, and the anti patterns imposed by mocking <a target="_new" href="http://www.disgruntledrats.com/?p=620">is given in this article</a>

A succinct description of the coupling issue <a target="_new" href="http://thought-tracker.blogspot.ca/2006/05/should-mock-objects-be-considered.html">is discussed here</a>

In addition to the issues described above, there are two pragmatic issues that affect my preference for mocking actually depend more on my current language of choice: Scala. One issue is that the most capable mocking framework I know of, Mockito, doesn&#8217;t play well with Scala &#8211; it can&#8217;t, for example, properly mock methods defined in a trait. As a result, because I TDD, I&#8217;m tempting to not use some of the more powerful features of Scala just because my mocking framework of current choice doesn&#8217;t handle them well. Of course, new frameworks coming along, like ScalaMock, might make this argument moot. When I found myself creating behaviour-less traits just to provide easier mocking in my tests, I realized there was a problem.

The other issue comes from the fact that it&#8217;s so darned easy to do stubs in Scala &#8211; given the low-ceremony ability to override and create closures and dynamic instances, it&#8217;s been my experience that mocks are actually more code and less comprehensible in Scala. This is not at all the case in Java, however, where mocks can be massively more succinct than stubs.

I subscribe to the original intent of object-orientation, which is that objects are encapsulations of state and behaviour, not data structures, and that the way to communicate between them is messages, not method calls. As a result, I find the verification of behaviour at the low level counterproductive. I prefer to verify the behaviour of objects (services, domain objects, etc) at a high level &#8211; e.g. does this thing DO what I want it to do, as opposed to asking &#8220;does it do the thing I&#8217;m testing the WAY I think it does&#8221;. These are two very different questions.

At the same time, I have a strong preference for functional programming, which also supports easier testing, making the issues of mocking less critical, as the stubs I need to test more fully functional code are trivial compared to what highly procedural code using mutable objects requires.

After all, why do we test? This is a larger question, and a topic for another blog post, but for me, the answer is two-fold: to give me confidence that the system does what I specify it to do, with some level of confidence, and to allow me to refactor freely and frequently while maintaining that confidence. As a result, the last thing I want to do is to ensure the system does what it does *the same way* it did it a minute ago &#8211; I don&#8217;t care how it does the thing it does, only that it does. In fact, I must *not* care about the how, or I can&#8217;t refactor without re-writing large hunks of my tests.

This preference to thinking about the *what* instead of the *how* is also, incidentally, what causes my preference for using Guice when managing services and dependency injection: because Guice allows me to quickly add new dependencies and change constructor signatures without having to go back and re-write tests, it allows me to go faster than manual module creation does, so I prefer it.

Whether I have annotations telling me my code is injected or a module class somewhere doing the injection manually for me is less interesting, although at least the annotations tell me *in the class I&#8217;m looking at* that dependency injection is taking place.

In any event, that preference is a side issue to the mocking/stubbing preference.

I hope this material provides some food for thought.

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