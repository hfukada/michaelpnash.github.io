---
title: Scala and Java Together
author: mnash
excerpt: Using Scala and Java together in software development
layout: post
permalink: /scala-and-java-together/
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
  - Concurrency
  - Java
  - Maven
  - Netbeans
  - Scala
---
Given a need to work towards more scalable systems, and to increase concurrency, many developers working in Java wonder what&#8217;s on the other side of the fence.

Languages such as Erlang and Haskell bring the functional programming style to the fore, as they essentially force you to think and write functionally &#8211; they simply don&#8217;t support (well, at least not easily) doing things in a non-functional fashion very easily.

The mental grinding of gears, however, can be considerable for developers coming from the Java (or C/C++) worlds in many cases, who have become familiar with the Object-oriented paradigm. An excellent solution might be to consider the best of both worlds: [Scala][1].

I had the opportunity this weekend to renew my acquaintance with Scala, and to work on blending it with the old mainstay, Java. Scala runs on the JVM, so as you might expect, it can be combined pretty readily with Java &#8211; more cleanly than before, given some new Maven and IDE plugins.

**  
IDE Support for Scala**  
My IDE of choice lately has been Netbeans, and sure enough, there&#8217;s a (beta) [Scala plugin for Netbeans][2]. 

Installing this plugin gives me syntax-aware editing of Scala source, along with basic refactoring support. Here&#8217;s the obligatory &#8220;Hello, World&#8221; in Scala sitting happily in my Netbeans window, color-highlighted syntax and all: 

![helloworld Scala and Java Together][3]

**Maven plugin**  
In order to organize my code, tests, and generally make life easier, I&#8217;ve used Maven to first generate the project, then created the code above (and some more, as we&#8217;ll see in a minute). I started with the regular &#8220;mvn archetype:generate&#8221; command to build my source directories just as for a Java project, then added a bit of Maven magic to the generated POM to use the [Maven Scala plugin][4]. Here&#8217;s the full POM:

![pompart1 Scala and Java Together][5]

Lines 21-25 tell Maven where to find the actual Scala plugin  
29-33 add the Scala libraries to our list of dependencies

![pompart2 Scala and Java Together][6]

Lines 44 thru 48 add the Scala plugin itself to our build lifecycle

![pompart3 Scala and Java Together][7]

Lines 58 thru 75 specify the lifecycle events we bind to for actually compiling first the Scala production code, then the tests.

When we open this POM with Netbeans, you&#8217;ll see we&#8217;ve got a folder defined for both our Scala sources and tests, and our regular folders for Java sources and tests:  
![scalaandjavainproject Scala and Java Together][8]

**Calling Scala code from Java code**

Now that we&#8217;ve got our project defined to contain both Scala and Java, let&#8217;s put them to work together. We can call our Scala code directly from Java just as if the objects involved were Java, like so:

`HelloWorld.main(null)`

The only class we&#8217;ve got defined with the name HelloWorld is the Scala version &#8211; but it looks like Java as far as our Java classes are concerned. (There are some things to keep in mind when doing more advanced types between the two, but if you keep your interfaces straightforward these edge cases don&#8217;t arise very often).

**Calling Java code from Scala code**

The reverse is also true: we can make use of the entire library of existing Java code out there from Scala, even easier than in the reverse direction, as the more sophisticated type system of Scala handles anything Java can throw at it. Let&#8217;s look at a good example: Using JUnit4 (a Java library) to test both Scala and Java code.

**Using JUnit4 to test Scala**

The simple and expressive [JUnit][9] library has implementations in a number of other languages, but in the case of Scala and Java, the connection is so close we don&#8217;t really need a Scala version at all &#8211; we can use JUnit directly from a test written in Scala, as described below.

**With the test written in Scala&#8230;**

Here we see a Scala test, DogTest, running from within Netbeans (using Maven). 

![dogtest Scala and Java Together][10]

(Yes, the DogTest class is actually defined in a file called AppTest.scala &#8211; perfectly valid in Scala)

The results can be seen in the lower window (printing &#8220;Hello, World&#8221;).

As you can see, we&#8217;re using JUnit4, even with it&#8217;s Annotations, despite the fact the test is written in Scala.

**With the test written in Java&#8230;**

Now let&#8217;s go the other way: This is simply a matter of writing a regular Java Junit4 test, except instead of calling a Java class we&#8217;re actually calling our Scala class again.

![apptestjava Scala and Java Together][11]

In this example, you can see we&#8217;re using JUnit 4 in the usual way, but on line 20 and 25 we make reference directly to Scala classes, just as if they were regular Java classes. (The IDE shows them underlined due to a classpath issue, but they compile just fine in any case &#8211; the Netbeans Scala support is still Beta, after all).

As you can see, these two languages blend very smoothly in many respects, even more so than one of my other favorite combinations, Java and JRuby.

Although it is cool to see Scala and Java in a single project, I probably wouldn&#8217;t do it this way for production code. A cleaner approach might be to write a pure Scala module that is then a dependency of the Java project (or vice-versa), using Mavens ability to handle cross-project SNAPSHOT dependencies to break our work up into more manageable chunks.

We can then call Scala functionality from any Java application, even webapps, while still working with all of the exact same tools and procedures we&#8217;re used to for pure Java projects. Of course, we can also go the other way: write Scala web applications (perhaps with the excellent [Lift framework][12]) and call existing Java functionality, just as easily. 

I predict Scala will be used in more and more Java (and other JVM-based language) projects where the advantages of functional programming and high concurency are necessary, while at the same time preserving the massive investment in Java many of us already have.

Long live the happy couple!

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

 [1]: http://www.scala-lang.org/
 [2]: http://wiki.netbeans.org/Scala
 [3]: http://50.116.19.42/wordpress/wp-content/uploads/2009/05/helloworld.jpg "Scala and Java Together"
 [4]: http://scala-tools.org/mvnsites/maven-scala-plugin/
 [5]: http://50.116.19.42/wordpress/wp-content/uploads/2009/05/pompart1.jpg "Scala and Java Together"
 [6]: http://50.116.19.42/wordpress/wp-content/uploads/2009/05/pompart2.jpg "Scala and Java Together"
 [7]: http://50.116.19.42/wordpress/wp-content/uploads/2009/05/pompart3.jpg "Scala and Java Together"
 [8]: http://50.116.19.42/wordpress/wp-content/uploads/2009/05/scalaandjavainproject.jpg "Scala and Java Together"
 [9]: http://junit.org/
 [10]: http://50.116.19.42/wordpress/wp-content/uploads/2009/05/dogtest.jpg "Scala and Java Together"
 [11]: http://php.jglobal.com/blog/wp-content/uploads/2009/05/apptestjava.jpg "Scala and Java Together"
 [12]: http://liftweb.net/