---
title: 'Other People&#8217;s Databases'
author: mnash
excerpt: "Accessing databases from other applications is a harmful practice, and much can be gained by not doing it, even if it's become an ingrained habit. In this post I explain why my team has adopted this rule, and what we get from it."
layout: post
permalink: /other-peoples-databases/
livefyre_version:
  - 3
categories:
  - Rant
  - Scalability and Performance
  - Software Design
---
<p style="text-align: left;">
  <a href="http://jglobal.com/wp-content/uploads/2013/06/photo-1-e1372347288945.jpg"><img class="size-medium wp-image-2351 alignright" alt="photo 1 e1372347259389 224x300 Other Peoples Databases" src="http://jglobal.com/wp-content/uploads/2013/06/photo-1-e1372347259389-224x300.jpg" width="224" height="300" title="Other Peoples Databases" /></a>My team has an elbow-length blue latex glove on the wall of our team area, with the words &#8220;other people&#8217;s databases&#8221; written on it.
</p>

This is our tongue-in-cheek reminder to always think twice before sticking your fingers (or more) into a database that doesn&#8217;t belong to your application.

I realized the other day that this is not a universal principle, and this came as a bit of a surprise to me. Maybe I&#8217;ve just lived with it as an axiom for so long, I assumed everyone else did as well.

### The Rule

What I mean by &#8220;other people&#8217;s databases&#8221; is the rule that I follow, and my team has adopted, that says each deployable service or application in our overall system must communicate with other services and applications via established APIs. In some cases, these are asynchronous events (messages) passed between applications via an event bus. In other cases they are REST calls that one application makes to another.

In all cases, the API is one piece of application code talking to another via some established protocol.

Under no circumstances is that communication via a database, because each of our applications treats it&#8217;s database (assuming it has one) as an *internal* implementation detail, subject to change without any notice or consideration for other applications.

If one of our services handles customers, for instance, it might write those customers into a file on the filesystem, it might write them to MongoDB as a document, it might create them by replaying a series of domain events from a journal, or it might hold them all in memory and hope like hell the power doesn&#8217;t fail. It is *not the business* of any external application *how* the customer service does these things. All the external apps know is the API that the customer service exposes.

This is critical, as it allows us to rapidly, easily and safely change anything about a service *except* it&#8217;s external interface. We can change the external interface too, it&#8217;s just that we must then consider all the callers to that interface and make the change on their end (or handle multiple versions of the interface temporarily, which is usually the case).

Just as you don&#8217;t want other classes to know the internal workings of any class in your system (the open/closed principle), but just to *use* that class via it&#8217;s exposed interface, so you also want your services and applications to follow the same rule.

### The Consequences

I&#8217;ve had some people tell me that they just *love* big monolithic databases that span multiple applications, that it helps them get stuff done. What I hear is that they love being able to bypass their applications logic and safeguards and muck with the critical, inner workings of the company&#8217;s lifeblood without so much as washing their hands.

Moving some of the applications logic *into* the database, via the abomination of stored procedures or triggers, makes a bad situation worse.

The symptom of this thinking is a gradual slow-down in the pace of change, and the increase in risk with each new feature that works on the same database. Bugs crop up in strange and subtle ways, as the data is squirming underneath the applications, which are now forced to endure anemic domains, as they can&#8217;t rely on any logic they put in their domain to actually do anything correctly. Over time, if you ask someone what their domain model is, they&#8217;ll point to their database schema. This is the terminal stage of the disease, if you&#8217;re not careful.

The schema ossifies, becoming harder and harder to change, and the release cycle slows down (if it wasn&#8217;t already slow) to allow for &#8220;scripts&#8221; or &#8220;jobs&#8221; to be run to further fiddle with data to make each modification to the code possible.

Cost of change skyrockets in this scenario.

The other cry I hear is &#8220;ad-hoc reporting&#8221;, but I&#8217;ve already <a href="http://jglobal.com/the-ad-hoc-reporting-problem/" target="_new">dealt with that red herring here</a> so I won&#8217;t repeat my reasoning.

My conclusion is that the so-called benefits of &#8220;sharing&#8221; a database are in fact flaws, and that they are serious and avoidable, especially in any system that needs and wants to continue to be maintainable over time.

Now, there are actual exceptions when it&#8217;s OK for two deployable units to be talking to the same database (a write model unit and a read model, for instance), but that&#8217;s a rare and carefully managed exception to the rule, and I&#8217;d recommend you not do it unless you have a team that can follow critical disciplines very carefully.

Keep your fingers out of other people&#8217;s databases, you&#8217;ll be glad you did!