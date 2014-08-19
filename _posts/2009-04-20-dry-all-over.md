---
title: DRY All Over
author: mnash
excerpt: "Don't Repeat Yourself"
layout: post
permalink: /dry-all-over/
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
  - configuration
  - design
  - DRY
---
**Dry defined**  
DRY is the acronym for Don&#8217;t Repeat Yourself. It applies **everywhere** when writing good software, so I think it bears further examination.

**Why Dry?**  
The rationale behind dry is more than just efficiency: It helps reduce bugs and problems by enabling you to solve each problem only once, and when there&#8217;s a new problem, finding the one and only place it needs to be solved, whether that problem is where to configure something, or a piece of code implementing a specific algorithm.

**Dry your code**  
When most developers think of DRY, it&#8217;s in relation to code, where you want to not repeat a specific piece of code too often &#8211; ideally no more than once. Some development languages and environments lend themselves better to this than others. In some languages and environments, you find that if you attempt to get too DRY, you end up making code that&#8217;s hard to read. 

A common example is with testing &#8211; if you abstract out everything in your tests until it hurts, you may find that you&#8217;ve made the test into a tangled web that requires reading 4 classes to understand. For example &#8211; you need test data set up, so you make a method in some super class called &#8220;setUpTestData&#8221;, then call it all over the place. The problem with this is that it&#8217;s not obvious what&#8217;s contained in that test data. Is the data appropriate to the test you&#8217;re writing? Dunno &#8211; you&#8217;ve got to go look in (at least) the super class to see where it&#8217;s defined. A better approach might be to DRY out in a mode DSL-like way with methods like so: createTestCustomer(name, id).withInvoices(invoiceNumber, amount).

Now you can see right in the code what&#8217;s going on, even though the details of actually *how* a customer (or an invoice) is created or related to one another are DRY-ed out into the parent class (or somewhere else). Sometimes (more rarely than it happens, IMO), this is a good place for a static method (but that&#8217;s a subject for a later rant) <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile DRY All Over" class="wp-smiley" title="DRY All Over" /> 

**Dry your design**  
It&#8217;s not just your code you can DRY out, however. You can also apply DRY principals to your design, as you go to build either a refinement to an existing system or a whole new system. Part of this is simply good systems design, and keeping Separation of Concerns in mind. Have one class (module, whatever the right thing in your language of choice is) do one thing and do it well. Don&#8217;t have it depend on too many other things, and above all, don&#8217;t have it depend on how those other things do *their* thing.

Then design for re-use, instead of having to have 14 different variations of every class to do things that are subtly different. Maybe a few of those variations are significant enough to warrant a new class, but most probably aren&#8217;t. There&#8217;s of course a fine line here between a flexible class that does one thing and a class that does more than one thing depending on how it&#8217;s called or it&#8217;s configuration. You want the former, never the latter. As soon as a class is clearly responsible for more than one area of concern, it should be broken up into more than one class &#8211; this actually *encourages* re-usability. There seems to be a natural level of granularity for every project, where classes are doing enough but not too much, to maximize re-use and, therefore, most DRY-ness.

**Dry your configuration**  
Configuration is another area that is very often forgotten when applying DRY. If you&#8217;ve got several different ways to configure your application, or, worse, only one way to configure each part, but each part is configured differently, then you are repeating yourself. I&#8217;d argue you might also have other design issues, because how a class is configured is generally not a concern of the class itself, but of the container or environment in which the class is deployed, but that&#8217;s also another topic.

If you see a situation where you need to use a system property to configure the database, but you need to put stuff in a properties file to set up something else, and still another bit is configured with an XML file, you&#8217;re probably looking at a non-DRY situation where the classes are ending up doing their own configuration, rather than driving that configuration into them from elsewhere. This is hard to DRY-out, not to mention being awkward to change later &#8211; and there&#8217;s *always* a &#8220;later&#8221; when you need to change it <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile DRY All Over" class="wp-smiley" title="DRY All Over" /> 

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