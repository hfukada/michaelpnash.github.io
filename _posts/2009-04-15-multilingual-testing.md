---
title: Multilingual Testing
author: mnash
excerpt: "A technique I've seen a lot in recent years, and I believe for good reason, is using one language (programming language, that is!) to test code written in another."
layout: post
permalink: /multilingual-testing/
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
tags:
  - context switch
  - easyb
  - framework
  - junit
  - multilingual
  - rspec
  - ruby
  - tdd
  - testing
---
A technique I&#8217;ve seen a lot in recent years, and I believe for good reason, is using one language (programming language, that is!) to test code written in another.

There are some non-obvious advantages to this that I&#8217;d like to explore a bit below, as well as some obvious (but perhaps less important) disadvantages.

On the downside, of course, you need a developer or team conversant in at least two different languages. This is more rare than you might think, although I think more experienced developers have the edge in that they&#8217;ve likely been working in more than one language if they&#8217;ve been in the industry a while. Also, many developers like to tinker, and will often pick up one of the &#8220;low ceremony&#8221; languages to do that tinkering with, and end up gaining at least a passing familiarity with a new language as a result.

Another downside (and often the reason this isn&#8217;t done more) is a lack of common tool support between the two languages. If you&#8217;re working in an IDE that only speaks Java fluently, for instance, you&#8217;re less inclined to use another language for your tests, as then you&#8217;ve not only got to switch languages, but endure the &#8220;context switch&#8221; overhead of changing IDE&#8217;s midstream as well. If you&#8217;re doing real TDD, that&#8217;s a lot of context switches.

On the upside, though, there are a number of good reasons you might want to consider using a different language for your tests:

*   Intentional context switch: The same reason some people avoid switching languages for testing can actually be an advantage. When you&#8217;re tests are in another language, you&#8217;ve got a built-in mental gear-change between the code and the tests
*   Decoupling: If you&#8217;re changing language, you&#8217;re more inclined (maybe even required) to limit the touch-points between the tests and the actual code &#8211; e.g. you might isolate the interface to a single class that&#8217;s made visible in the test. This can be a good thing, as a too-tightly coupled test is a brittle test (and often not a unit test, but that&#8217;s a whole &#8216;nother topic)
*   Better test framework: While xUnit-like frameworks abound in just about every language, some of the higher-level and BDD-type frameworks are best in one specific language. [RSpec][1] is an excellent example: It&#8217;s originally in Ruby (although I understand some attempts have been made to port it), so it might be that you&#8217;d consider using Ruby as a test language in order to get the goodness of RSpec. Ditto for [easyb][2], which is written in Groovy (a very close relative of Java, in many ways). 
    The reverse could be true: You could write JUnit unit tests for your Scala application, for instance, taking advantage of JUnit 4 and friends being on the Java platform. </li> 
    *   Better language suitability: Some languages are much &#8220;lower ceremony&#8221; than other &#8211; e.g. compare Ruby and Java. You need a lot of scaffolding and fuss around a large Java application, but Ruby is a bit more nimble and in some cases, more expressive. Expressiveness being a key quality of a good test, this might mean testing a Java app with Ruby (or perhaps JRuby, to be specific) is a good plan, especially with the existence of Test::Unit and RSpec and such
    *   Multi-Lingual project: It&#8217;s becoming more and more common to see a project use more than one development language in any case (e.g. for the &#8216;real&#8217; code, not just the tests). In this case, there&#8217;s even less of a barrier to doing your tests in one of those languages &#8211; you&#8217;re only helping to maintain your fluency in both language as well, which can&#8217;t be a bad thing.</ul> 
    So, how about it? Anyone out there have good or bad stories about multi-lingual testing to share?
    
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

 [1]: http://rspec.info/
 [2]: http://www.easyb.org/