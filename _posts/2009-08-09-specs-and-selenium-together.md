---
title: Specs and Selenium together
author: mnash
layout: post
permalink: /specs-and-selenium-together/
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
  - Software Testing
  - Tips and Tricks
tags:
  - integration
  - Java
  - Scala
  - selenium
  - testing
  - webapps
---
I recently had the chance to dive into a new project, this one with a rich web interface. In order to create acceptance test around the (large and mostly untested) existing code, we&#8217;ve started writing [specs][1] acceptance tests.

Once we have our specs written to express what the existing functionality is, we can refactor and work on the codebase in more safety, our tests acting as a &#8220;motion detector&#8221; to let us know if we&#8217;ve broken something, while we write more detailed low-level tests (unit tests) to allow easier refactoring of smaller pieces of the application.

What&#8217;s interesting about our latest batch of specs is that they are written to express behaviours as experienced through a web browser &#8211; e.g. &#8220;when a user goes to this link and clicks this button on the page, he sees something happen&#8221;. In order to make this work we&#8217;ve paired up specs with [Selenium][2], a well-known web testing framework.

By abstracting out the connection to Selenium into a parent Scala object, we can build a DSL-ish testing language that lets us say things like this:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
object AUserChangesLanguages extends BaseSpecification {

  "a public user who visits the site" should beAbleTo {
    "Change their language to French" in {
      open("/")
      select("languageSelect", "value=fr")
      waitForPage
      location must include("/fr/")
    }
    "Change their language to German" in {
      select("languageSelect", "value=de")
      waitForPage
      location must include("/de/")
    }
    "Change their language to Polish" in {
      select("languageSelect", "value=pl")
      waitForPage
      location must include("/pl/")
    }
  }
}
&lt;/code&gt;
</pre>
</div>

This code simply expresses that as a user selects a language from a drop-down of languages, the page should refresh (via some Javascript on the page) and redirect them to a new URL. The new URL contains the language code, so we can tell we&#8217;ve arrived at the right page by the &#8220;location must include&#8230;&#8221; line.

Simple and expressive, these tests can be run with any of your choice of browsers (e.g. Firefox, Safari, or, if you insist, Internet Explorer).

Of course, there&#8217;s lots more to testing web pages, and we&#8217;re fleshing out our DSL day by day as it needs to express more sophisticated interactions with the application.

We can get elements of the page (via Xpath), make assertions about their values, click on things, type things into fields and submit forms, basically all the operations a user might want to do with a web application.

There are some frustrations, of course. The Xpath implementation on different browsers works a bit differently &#8211; well, ok, to be fair, it works on all browsers except Internet Exploder, where it fails in various frustrating ways. We&#8217;re working on ways to overcome this that don&#8217;t involve having any &#8220;if browser == &#8221; kind of logic.

It&#8217;s also necessary to start the Selenium RC server before running the specs, but a bit of Ant magic fixes this.

We&#8217;ve got these specs running on our TeamCity continuous integration server, using the TeamCity runner supplied with Specs, where we get nicely formatted reports as to what&#8217;s pending (e.g. not finished being written yet), what&#8217;s passing, and what&#8217;s failing.

The specs written with Selenium this way are also a bit slow, as they must actually wait in some cases for the browser (and the underlying app!) to catch up. When run with IE as the browser, they&#8217;re more than just a **bit** slow, in fact&#8230;

They are, however, gratifyingly black-box, as they don&#8217;t have any connection to the code of the running application at all. For that matter, the application under test can be written in any language at all, and in this case is a combination of J2EE/JSP and some .NET.

There&#8217;s a lot of promise in this type of testing, even with it&#8217;s occasional frustrations and limitations, and I suspect we&#8217;ll be doing a lot more of it.

 [1]: http://code.google.com/p/specs/
 [2]: http://seleniumhq.org/