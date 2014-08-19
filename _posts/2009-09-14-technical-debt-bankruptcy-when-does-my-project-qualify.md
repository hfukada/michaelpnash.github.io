---
title: 'Technical Debt Bankruptcy: When does my project qualify?'
author: mnash
excerpt: How do I know when putting more resources into a software project is counterproductive?
layout: post
permalink: /technical-debt-bankruptcy-when-does-my-project-qualify/
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
  - Bankruptcy
  - technical debt
---
In my last [post][1], I discussed the concept of &#8220;technical debt bankruptcy&#8221;, a term for when you make the informed decision that a particular piece of software is costing more to maintain than it would cost to re-write.

Two closely related concepts are how to determine exactly and safely when this point has arrived, and how to handle the &#8220;restructuring of debt&#8221; that comes with the technical equivalent of a chapter 11 re-organization.

As a colleague pointed out in a comment about the last post, you can&#8217;t simply ignore the baked-in business value in the old solution. If you&#8217;re considering re-writing it, instead of just turning it off, then there must be someone using it for a valuable purpose. 

First, though, you must be able to determine if your project (or some part of it) &#8220;qualifies&#8221; for such a process. Some projects don&#8217;t lend themselves to a proper restructuring, and might simply need to be put out of their (and your) misery, if the business value has evaporated. 

This requires measuring, not guessing, even though sometimes there are items involved that are hard to measure.

Some of the things you need to measure are:

1. What is the current business value? This involves asking who uses the feature, how much, and what is it&#8217;s relative importance in the overall project. Sometimes it is difficult to get objective metrics on this, but that&#8217;s what&#8217;s needed to make an informed decision as opposed to a guess. 

Gut feel does not count as a metric &#8211; you need to know who is using the system, how often, and for what purpose. Then you can determine if that purpose is equally well or better served by some other system, allowing that user to be weaned off the legacy system under consideration.

If you have logging or other metrics of use being gathered on the old system, this can be a good place to start, although you may need to augment the current metrics to get a baseline. Be sure that you&#8217;re looking at a long enough period to get a real picture, as often legacy systems have very intermittent use patterns.

2. What are the features, exactly? The best way to determine this is to write behavior-driven decoupled functional tests around the features of the system under consideration. 

What I mean here is a list of scenarios that describe use cases of the feature in question, along with executable specifications for each such case, written so that they do not have any dependencies directly on the code under test. 

Like all good tests, they need to be repeatable, atomic (at least at the whole scenario level), and automated. One example might be Selenium/Specs tests that exercise a feature of a web application by simulating a user interacting with the application from a browser. The tests must reflect how the feature is **actually** used, not how it was intended to be used, as often in legacy apps these are not at all the same thing.

3. The cost to re-write (or &#8220;aggressive refactoring&#8221;, as you might call it, given that there are existing functional tests). 

This is a tough one, as often the technologies and techniques that might be used for a rebuild of an existing system are very different from those that were used in it&#8217;s original construction &#8211; especially if a lot of time has passed. Web and application development techniques have come a long way since, for instance, JSP 1.0, and the amount of effort to get an operational application is massively smaller than it used to be.

You need to estimate carefully, referring to the functional tests as the specification for the new system to be built. Once those functional tests are passing against the re-write, then you have, by definition, replaced the old system with the old, as the functional tests provide the full definition of what needs to be re-written. Don&#8217;t gold-plate, and don&#8217;t neglect to cover every valuable feature with the functional tests.

Now it&#8217;s down to the hard numbers: Let&#8217;s say that the old system takes 500 units (of something) to implement a new feature, on average. If we have 10 features in our backlog, our estimated total cost is then 5000 units.

If our new system will take 2000 units to build, and the cost of a new feature is then 50 units (and this is a very reasonable ratio, in my experience), then the math works out like so:

Total forecast for adding our backlog to the old system: 5000 units.

Total forecast for creating the new system and building the 10 features in the backlog: 2500. 

This step is often made harder by the fact that some of the stakeholders in a project may not fully understand or have faith in either the estimates or the functional tests. 

If they don&#8217;t have faith in the functional tests, then they must be able to read them and point out where the test doesn&#8217;t cover a valuable use-case. If they can&#8217;t, then they must accept that the tests do in fact specify the system adequately.

The estimates are another matter &#8211; often stakeholders won&#8217;t understand how large an advantage modern tools and techniques can offer, and find it difficult to believe that for the cost of a few bugs fixes or new features you can actually entirely replace a running legacy application. This is where non-technical stakeholders must have enough confidence in the professionalism and expertise of their developers &#8211; and nothing can substitute for that.

4. Conclusion

Now we have to take into account elements like migration of users from the old system to the new, data transfer (if any &#8211; perhaps the new system can be built on the same database as the old, in which case this doesn&#8217;t cost anything). Assuming these are, let&#8217;s say, 500 units (and that&#8217;s a lot, proportionally), we are still 2000 units ahead of the game with our current backlog, and that&#8217;s not considering if the new system costs less to deploy and/or operate than the old one. If it does, then the decision is even easier.

Of course, once the current backlog is handled, all future features have a 10 to 1 advantage over maintenance on the new system as well, which is where the real long-term massive savings come into play &#8211; not to mention the developer satisfaction, lower defect rate, and so forth.

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

 [1]: http://php.jglobal.com/blog/?p=525