---
title: First Look at Vaadin
author: mnash
layout: post
permalink: /first-look-at-vaadin/
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
  - Java
  - Scala
  - Vaadin
---
I&#8217;ve had the chance over a recent weekend to have a first crack at a web framework called [Vaadin][1].

I was originally browsing for news about the latest release of Google&#8217;s [GWT][2] framework when I stumbled on a reference to Vaadin, and decided to go take a look. What I found intrigued me, and I decided to take it for a test drive, as I was down sick for a couple of days with a laptop nearby&#8230;. My back became annoyed with me, but it was worth it, I think.

**First Look**  
First off, the practicalities: Vaadin is open source, and with a reasonable [license][3], the Apache License. The essential bits of Vaadin are contained in a single JAR, and it&#8217;s both Ant and Maven friendly right out of the box. 

The next thing that struck me about Vaadin was the documentation. The first unusual thing about it&#8217;s documentation was the fact of it&#8217;s existance, as open source projects are downright notorious for poor documentation. Vaadin is a pleasant exception, with tons of examples, a well-organized [API doc][4], in the usual JavaDoc format, and even the &#8220;Book of Vaadin&#8221;, [an entire PDF book][5] (also available in hardcopy) that takes you through Vaadin in enough detail to be immediately productive.

Given that surprisingly pleasant start, I dug deeper, creating a little app of my own. 

**Just the Java, Ma&#8217;am**  
The main thing that kept me interested in Vaadin once I started digging further was that it&#8217;s pure Java. Many frameworks talk about writing your UI work in Java, such as Wicket, but there&#8217;s still a corresponding template and some wiring that happens to put the code and the template together. Not so with Vaadin.

When they say &#8220;just Java&#8221;, they mean it &#8211; your entire UI layer is coded in Java, plain and simple. No templates, no tag libraries, no Javascript, no &#8216;nuthin. It&#8217;s reminiscent of the [Echo framework][6], except in Vaadin&#8217;s case the Javascript library that your code automatically produces is Google&#8217;s GWT, instead of Echo&#8217;s own Core.JS library.

Unlike GWT, though, the Vaadin approach doesn&#8217;t bind you to any specific source code though, it&#8217;s just a binary jar you put on your classpath. 

The **only** thing in my sample app, other than 2 Java files, was a web.xml and a css stylesheet, both of which were only a few lines long. And this was no &#8220;Hello, World&#8221;, either, but a rich AJAX webapp with a tree menu, fancy non-modal &#8220;fading&#8221; notifications, images, complex layouts, and a form with build-in validation. And it took maybe 4 hours of total work to produce &#8211; and that was from a standing start, as I&#8217;d never heard of Vaadin before last Thursday. Not bad, not bad at all.

I found I was able to get a very capable little webapp up and running with no need to invent my own components, even though I had trees and sliders and menus and other assorted goodies on the page. It worked in every browser I was able to try it in, which is certainly not the case for my own hand-rolled JavaScript most of the time <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile First Look at Vaadin" class="wp-smiley" title="First Look at Vaadin" /> 

I haven&#8217;t yet tried creating my own custom components, but it certainly looks straightforward enough.

I did try linking to external resources, and included non-Vaadin pages in my app, with no difficulties, so it appears that Vaadin plays well with others, and can be introduced into an existing project that uses, for instance, a whack of JSP&#8217;s that one might want to obsolete.

**Webapps**  
I think Vaadin warrants more exploration, and I intend to put it further through its paces in the next few weeks. It appears extremely well-suited to web applications, as opposed to websites with a tiny bit of dynamic stuff in them. 

It offers an interesting alternative to some of the patterns I&#8217;ve seen for advanced dynamic webapp development so far. 

One approach I&#8217;ve seen a lot is to divide the duties of creating an app into the &#8220;back end&#8221; services and the &#8220;UI&#8221;. Generally the UI is written in either JavaScript, or uses Flex or some other semi-proprietary approach. The &#8220;back end&#8221; stuff is frequently written to expose it&#8217;s services as REST, then the two are bolted together. The pain point here happens when the two meet, as it&#8217;s common and easy to have minor (or major!) misunderstandings between the two teams. This usually results in a lot of to-and-fro to work out the differences before the app comes all the way to life.

The other approach, more common on smaller or resource-strapped teams, is to have the same group responsible for both UI and back-end services. This reduces the thrash in the joints a bit, but doesn&#8217;t eliminate it, because the two technologies on the two sides of the app aren&#8217;t the same. You can&#8217;t test JavaScript the same way you write Java, for instance, and they&#8217;re two different languages &#8211; one of which (Java) has far better tooling support than the other. IDE support, for instance, is superb for Java, and spotty at best for JavaScript.

With Vaadin, both of these approaches become unnecessary, as its the same technology all the way through (at least, what you write is &#8211; technically it&#8217;s still using JavaScript, but because that&#8217;s generated, I don&#8217;t count it).

You get to use all of the tools you know and love for the back-end services to write the code for the UI, which you can then unit and functional test to your heart&#8217;s content.

The temptation to mix concerns between UI code and back-end service code must still be resisted, of course, but at least that code isn&#8217;t buried somewhere in the middle of a JSP page, ready to leap out and bite you later.

Because you&#8217;re using dynamic layouts, the app always fits properly on the screen without any extra work, addressing a pet peeve of mine, the &#8220;skinny&#8221; webapp, restraining itself to the least common denominator of screen size, thus rendering impotent my nice wide monitors.

**Scala**  
Just because Vaadin is a Java library doesn&#8217;t restrict you to using Java to drive it, however. I made another little webapp where the whole UI was defined in Scala, calling the Vaadin APIs, and it worked like a charm. In some ways, Scala is an even better fit for Vaadin than straight Java, I suspect. I haven&#8217;t tried any other JVM compatible language, but I see no reason they wouldn&#8217;t work equally well.

**Deployment and Development Cycle**  
As I was building the app with Maven, I added a couple of lines to my POM and was able to say &#8220;mvn jetty:run&#8221; to get my Vaadin app up and running on my local box in a few seconds. My development cycle was only a few seconds between compile and interactive tests, as I was experimenting with the trial-and-error method. 

TDD would be not only possible, but easy in this situation.

I successfully deployed my little Vaadin app to ServiceMix, my OSGi container of choice, without a hitch. 

Performance appeared excellent overall, although I haven&#8217;t formally tested it with a load-testing tool (yet).

**Summary**  
So far, I&#8217;m impressed with Vaadin. I&#8217;m more impressed with any web framework I&#8217;ve worked with in a number of years, in fact. I&#8217;m sure there are some warts in there somewhere, but for the benefits it brings to the table, I suspect they&#8217;re easily worth it. I think the advantages to teams that already speak fluent Java is hard to overstate, and the productivity to produce good-looking and functioning webapps is quite remarkable.

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

 [1]: vaadin.com
 [2]: http://code.google.com/webtoolkit/
 [3]: http://vaadin.com/license
 [4]: http://vaadin.com/api/
 [5]: http://vaadin.com/book
 [6]: http://echo.nextapp.com/site/