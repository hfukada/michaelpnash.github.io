---
title: 'Putting the &#8220;fun&#8221; back in Functional Testing'
author: mnash
layout: post
permalink: /putting-the-fun-back-in-functional-testing/
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
  - automated
  - Concurrency
  - Grid
  - HtmlCleaner
  - Internet Explorer
  - Java
  - jaxen
  - Scala
  - selenium
  - Selenium Grid
  - specs
  - testing
  - xml
  - xpath
---
Another update in our team&#8217;s journey to functional testing nirvana via [Specs][1] and [Selenium][2]. <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Putting the fun back in Functional Testing" class="wp-smiley" title="Putting the fun back in Functional Testing" /> 

We discovered an earth-shattering revelation (not): Internet Explorer Sucks. Unfortunately, it&#8217;s the &#8220;target&#8221; browser for a certain project we&#8217;re working on, therefore we&#8217;re stuck with it. Being stuck with it means finding a way to make it suck sufficiently less that it will actually run our lovely tests, which Firefox (and several other browsers) digest quite happily.

One way in which IE sucks is that it&#8217;s painfully slow &#8211; test that take a few seconds on Firefox timeout after several minutes in IE. If you keep cranking out the timeout they might eventually pass, but we want test results in our lifetimes, so we set about finding a way to get our feedback out of IE a bit faster. 

It turns out one of the very slow things about IE is asking for an element via an xpath, and we were doing this a lot. We tried reducing the number of places we did this, and indeed that helped a bit, but there were some things on our existing app that were really hard to refer to without xpath. To ease the pain further, we took a slight detour. Instead of asking Selenium for a specific xpath, which then caused Selenium to ask the browser, we fetched the entire output of the browser (via the getHtmlSource method in Selenium). 

What we&#8217;d like to do instead, where possible, is simply make assertions on the XML of the entire page &#8211; so we get it just one time, and so that we don&#8217;t depend on the Xpath implementation of the browser to find bits of our page for us.

Unfortunately, we still can&#8217;t ask anything xpath-ish of it, as although it bears a close resemblance to XML, it&#8217;s not **really** html, so any parser we could find choked on it.

Enter [HtmlCleaner][3] a handy little jar that can digest even the most disguisting HTML and deposit clean shiny XML in it&#8217;s place. Now we could take our XML version of what the browser spat out and finally make Xpath calls to it.

Now Scala itself has excellent support for XML ([see the whole book here][4]), but it&#8217;s support for Xpath is&#8230; interesting. Xpath is actually done via a series of methods and functions, meaning although it is very powerful, it&#8217;s not the **same** xpath as you might be used to, or, more importantly in our case, not the same as you could expect a browser to understand. This means we could either re-write all our Xpath queries (and make it harder to use Selenium IDE or Firebox to help us write new ones), or find another way&#8230;

Enter [Jaxen][5], a handy Java lib with full Xpath support, without all the weight of other solutions. Of course, as Specs is written in Scala and Scala happily uses any existing Java lib, we could just drop a jar into our &#8220;lib&#8221; dir and work some magic.

We needed to convert the HTML produced by Selenium into XML, then turn it into a DOM document that Jaxen can process, so we can ask questions in xpath of the resulting Jaxen document.

This little incantation:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
 val cleanerAndProps = initCleaner

  private def initCleaner = {
    var cleaner : HtmlCleaner = new HtmlCleaner();
    var props : CleanerProperties = cleaner.getProperties();

    props.setTranslateSpecialEntities(true)
    props.setRecognizeUnicodeChars(true)
    props.setOmitComments(true)
    (cleaner, props)
  }
&lt;/code&gt;
</pre>
</div>

Returns a tuple of the HtmlCleaner instance and it&#8217;s properties, which we can then use for our conversion somewhat like so:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
def getHtmlText(element: String) = {
      var node : TagNode = cleanerAndProps._1.clean(selenium.getHtmlSource())
      val domSerializer: DomSerializer = new DomSerializer(cleanerAndProps._2)
      val document: org.w3c.dom.Document = domSerializer.createDOM(node)
      val xpath = new DOMXPath(element)
      xpath.stringValueOf(document)
  }
&lt;/code&gt;
</pre>
</div>

This method then takes a string (actually an xpath query), &#8220;cleans&#8221; the HTML from Selenium, then serializes it into a DOM (a regular org.w3c.dom.Document), allowing us to use Jaxen&#8217;s DOMXpath object to fish out the string value of whatever our Xpath query returns, allowing us to say things like:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
manufacturerSelected = getHtmlText("//table[@class=&#039;DataList&#039;]//a")
&lt;/code&gt;
</pre>
</div>

In our tests.

Of course, we can dress this with other methods that get attributes and other things from the DOM tree, but you get the point.

The nice part about all this is that it doesn&#8217;t require a new round trip to the browser &#8211; we can assert as many things as we want and fish out as many values as we need directly from the resulting page in milliseconds now, instead of several seconds (or worse for IE) before.

So now we can run our tests much faster than before &#8211; but we&#8217;re writing a **lot** of tests, so it&#8217;s going to get slow again if we can&#8217;t scale better, even with the optimization with Jaxen and HtmlCleaner.

So we looked into [Selenium Grid][6]. Before, we had our Ant script that ran the tests (whether locally or on TeamCity), fire up a Selenium RC Server before the run, and shut it down again afterwards. This was time consuming, and problematic as we added more suites of tests. We wanted our tests to be able to run all at the same time, but each Selenium server (which does the communicating with the browser), needs to be on a different port for this to happen. Gah &#8211; this was getting complicated.

Selenium Grid, however, address this problem and several more at once.

It allows you to start a single &#8220;Hub&#8221; server, on one port (4444 by default). This hub then redirects load from tests to one of a number of actual Selenium RC servers that you fire up and leave running long-term.

In our case, we started 3 RC servers to talk to FireFox, and one for IE (it&#8217;s not a good idea to run more than one IE RC server on a single machine, as IE doesn&#8217;t play nice with other IE&#8217;s). 

Then on other VM&#8217;s we can fire up even more RC servers &#8211; both IE and FireFox flavors. Selenium Grid gives you a nice control panel to see the servers and which ones are available, and you can add new servers (and remove them) while the grid is up.

The max number of test runs you can have going at once is now the total number of Selenium RC servers in your grid, allowing many short sets of tests to all run at once, giving much faster actual elapsed time before you get feedback when something breaks.

Of course, one of the benefits of this new approach with Selenium Grid is that I can now test if something works via IE on Windows &#8211; from my Mac! For that matter, any combination of browsers and operating systems that we&#8217;ve got an RC server for can be tested, all at once. Good stuff.

There are still plenty of frustrations in this process &#8211; if you kill a test suite before it finishes, for instance, it appears that the Selenium RC server it was talking to remains unavailable forever, and when you restart the hub, you have to restart **all** of the RC servers&#8230; but it&#8217;s a step up from where we were.

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

 [1]: http://code.google.com/p/specs/
 [2]: http://seleniumhq.org/
 [3]: http://htmlcleaner.sourceforge.net/
 [4]: http://burak.emir.googlepages.com/scalaxbook.docbk.html
 [5]: http://jaxen.codehaus.org/
 [6]: http://selenium-grid.seleniumhq.org/