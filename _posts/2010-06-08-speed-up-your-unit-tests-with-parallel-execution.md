---
title: Speed up your Unit Tests with Parallel Execution
author: mnash
excerpt: "I recently had occasion to use a trick with test execution that is simple and very helpful, but that I forget about frequently, so I thought I'd pass it alo ..."
layout: post
permalink: /speed-up-your-unit-tests-with-parallel-execution/
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
  - automated
  - Concurrency
  - Java
  - Maven
  - parallel
  - stateless
  - surefire
  - testing
  - threads
---
I recently had occasion to use a trick with test execution that is simple and very helpful, but that I forget about frequently, so I thought I&#8217;d pass it along here.

We use Maven to execute our unit (and sometimes functional, but that&#8217;s another story) tests for a suite of applications my team works on. Some of our apps have quite a few tests, and even though each unit test is very fast (as good unit tests ought to be), running that many of them still takes a bit of time. We&#8217;re also burdened with a very slow CI server, unfortunately, which aggravates that situation.

Unit tests, by definition, do not rely on the operation of any other test &#8211; they are self-contained, stateless and repeatable. This means they&#8217;re ideally suited to running in parallel, and fortunately, that&#8217;s very easy to do with Maven.

Maven uses the [Surefire Plugin][1] to do it&#8217;s test-running, and it&#8217;s configurable to run tests in parallel. Our project uses a parent pom (different from an aggregator pom) to specify common configuration, so our pom files stay lean. In our parent pom, we just add the following:

<pre class="brush:xml">&lt;plugin&gt;
  &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
  &lt;artifactId&gt;maven-surefire-plugin&lt;/artifactId&gt;
  &lt;version&gt;2.5&lt;/version&gt;
  &lt;configuration&gt;
    &lt;parallel&gt;methods&lt;/parallel&gt;
    &lt;threadCount&gt;20&lt;/threadCount&gt;
  &lt;/configuration&gt;
&lt;/plugin&gt;
</pre>

And we&#8217;ve told Maven to run our tests in a maximum of 20 threads, and to make each method run in parallel. (There are other options here for only running classes in parallel, etc, which might be helpful for functional tests).

Just doing that took a minute off the time of a couple of our builds, and a bit off the time of even some of the smaller ones. Of course, it&#8217;s even more effective if you&#8217;re running on a multicore machine, but even the feeble VM running our CI was faster with it there.

Enjoy!

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

 [1]: http://maven.apache.org/plugins/maven-surefire-plugin/index.html