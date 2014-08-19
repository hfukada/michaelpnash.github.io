---
title: Scala Continuous Testing with sbt
author: mnash
excerpt: Continuous testing is a method of re-running tests in an application whenever the code changes, automatically. Here we explore how to do this with Scala.
layout: post
permalink: /scala-continuous-testing-with-sbt/
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
  - Software Design
  - Uncategorized
---
I&#8217;ve recently had occasion to start an [open source project][1], and the correct tool for the job appears to be Scala. 

So far the project is going well, but the pain has been around the build and IDE support for rapid and convenient development in Scala. Although all three of the major IDEs I&#8217;ve worked with recently (Eclipse, IntelliJ IDEA and Netbeans) have plugins for Scala, they are all early releases, and have various degrees of pain associated with them.

I ended up using Netbeans for editing and as a subversion client, then building with Maven when I wanted to compile and/or run tests. Calling Maven from within Netbeans to build a Scala project is still a bit creaky, so I was doing it from a terminal window directly.

This is very inconvenient, for a number of reasons. First, I&#8217;m working in a Behaviour-Driven Development mode, using specs as my BDD framework. This means I first write a specification in specs, see it fail, then write the code necessary to make it pass, then write (or extend) the next specification for the next behaviour I want, and so forth.

When I want to run a test, I had to flip to a command window, issue a Maven command to build and select the specified test to run, something like this: 

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
mvn -Dtest=foo test
&lt;/code&gt;
</pre>
</div>

In order to make this work I had to declare my specs as JUnit tests (with the @Test annotation), even though they don&#8217;t use anything else from JUnit. This felt like a bit of a hack, albeit a useful one. Another pain point was the startup time for Maven (although I understand there&#8217;s a &#8220;console&#8221; plugin for Maven as well that can perhaps reduce this particular pain).

As I like to tinker with new stuff, I thought I&#8217;d make a departure from Maven and give [sbt][2] a try. [Sbt][2] is a build tool written in Scala that supports building both Scala and Java (and mixed) projects in a very simple way. Unlike Ant, there&#8217;s no up-front pain to write a build script, though, as sbt can make reasonable assumptions (which you can override) about where to find your classes and libraries, so you hit the ground running.

In literally seconds I was up and running after following the install instructions on the sbt site. After a bit of experimenting I found the &#8220;console&#8221; mode in sbt, where you launch sbt and leave it running. 

Once in console mode you can either just type &#8220;test&#8221; every time you want to build and run all tests, or be more selective, and run only the tests that failed last time, or just a single specified test, if you&#8217;re working on just one feature. Any of these operations are fast &#8211; mostly because sbt is already loaded and running, but also because sbt does a bit less work then Maven does on every build.

Although sbt can be configured to work in conjunction with Ivy or Maven repositories, you can also just drop your dependency libs in to &#8220;lib&#8221; directory in your project. For open source this is rather nice, as it saves the user of the project the trouble of trying to find them. Even supplying a Maven pom that specifies the repositories from which to download your dependencies is not a guarantee, as repositories change over time. Many is the time I&#8217;ve gone to download a dependency (or rather, Maven has gone to do it for me), only to find it&#8217;s not where it used to be, is a different name or version, or some other problem causes my build to fail. Like Ant, sbt can avoid this problem by keeping dependencies locally. Unlike Ant, it can also go get the dependencies the first time for you from the same repositories Maven uses &#8211; perhaps giving you the best of both words in some situations.

Even more interesting was the command 

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
~ test
&lt;/code&gt;
</pre>
</div>

Which runs all the tests, then waits for any source code to change (test or main code). When it sees a change, it runs all the tests again (after compiling the changes, of course). Poor mans continuous testing <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Scala Continuous Testing with sbt" class="wp-smiley" title="Scala Continuous Testing with sbt" /> 

Wait, it gets even awesomer! When you say 

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
~ test SomeTest
&lt;/code&gt;
</pre>
</div>

sbt will wait for any changes, then run just the specified test. This is ideal when you know you&#8217;re only working on a specific set of functionality (and therefore affecting only a single test). When sbt is waiting, you can just hit any key to return to the interactive mode, so it&#8217;s easy to change it from one of these modes to another.

Other commands in sbt are also very familiar and quick, such as &#8220;compile&#8221;, which does exactly as you&#8217;d expect from the name. &#8220;Package&#8221; is another good one &#8211; it produces a jar artifact, just like the Maven command of the same name. I haven&#8217;t yet tried it&#8217;s deploy mechanisms properly, but early results look promising.

I also like the &#8220;console&#8221; command, which runs the Scala command-line console, but with your project on the classpath, along with all it&#8217;s dependencies. This lets you do ad-hoc statements quickly and easily, and see the results right away. When you&#8217;re not sure what&#8217;s going on with a failing spec, I&#8217;ve found this mode very helpful to experiment. Scala is such an expressive language, I can write a quick experiment in one or two lines of code, see the result (as the Scala console also evaluates expressions by default), and go back to coding and testing, all without re-starting sbt. Quite nice, and somewhat reminiscent of the similar functionality in Rails and &#8220;irb&#8221; (and JRuby&#8217;s equivilant, Jirb).

There are many other things I&#8217;ve found about sbt that I like so far, but those are topics for another post later on&#8230;.

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

 [1]: http://code.google.com/p/cyberdyne/
 [2]: http://code.google.com/p/simple-build-tool/