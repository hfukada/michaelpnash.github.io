---
title: Production-Ready
author: mnash
excerpt: What does production-ready really mean for a software system?
layout: post
permalink: /production-ready/
categories:
  - Software Craftsmanship
---
I recently had a question asked of me, and I realized the answer to it is not as straightforward as I might have thought.
{{ /wp-content/uploads/2013/05/Anonymous_work_in_progress-e1403485244746.png }}

The question was &#8220;how should we determine if this software system is production-ready?&#8221;.

It turns out there are a number of different dimensions to this question, and I started enumerating them.

Of course, first we need to define &#8220;production ready&#8221; a bit more. I take it to mean that our system in it&#8217;s entirety is ready to put in front of &#8220;real&#8221; users &#8211; e.g. not alpha users or even beta users, but users that perhaps have paid, possibly a lot, to use this system, and have an expectation of it behaving well and correctly, and continuing to do so for as long as they choose to use it.

I don&#8217;t think these are in any particular order:

### The Code

In any software system there is a certain amount of cruft that builds up, even in a new system &#8211; a module we&#8217;re not quite happy with, a few lingering TODOs that haven&#8217;t quite been addressed, a refactor that should really be done. A pre-release code review, however informal, can help remind us of the state of pieces of our system that might require a bit more attention before our confidence is high enough to put it in front of it&#8217;s audience, so a code review is probably a good idea when considering production readiness.

### The Tests

Although really a part of &#8220;the code&#8221;, I&#8217;ll consider tests separately here. Wether the test suite is build using TDD, or after-the-fact, whether it&#8217;s mostly unit test, mostly integration tests, or something in between, these are all part of a bigger question: Do your tests give you confidence in the code?

Not just confidence in the part that&#8217;s tested (assuming it&#8217;s less than all of it), but in the **whole** system? If not, then I would contend you don&#8217;t quite have your testing strategy where it needs to be.

Assuming you do have what you consider to be confidence-ensuring tests, do they run regularly &#8211; e.g. every time anyone changes any part of the code or the system? If not, then again, you might be being deceived into a false sense of confidence, because what you&#8217;re saying is that there&#8217;s a way for changes to sneak around the tests &#8211; and as we all know, the tiniest most innocuous change can bring a system down hard and fast.

The whole &#8220;testing pyramid&#8221; must be considered here &#8211; unit tests alone can never give enough confidence in a system to say it is &#8220;production ready&#8221;, and exploratory tests alone are also woefully inadequate.

A final part of testing for production readiness has to be load and performance tests (which are not at all the same thing). These must be tailored to the specific system under test and it&#8217;s expected user requirements, of course &#8211; there&#8217;s no need to verify that a system that has an intended audience of 100 users can handle a million users. On the other hand, it&#8217;s always smart to test for a higher load than you anticipate &#8211; many SaaS systems today support self-registration, so user load can spike without any warning and without your consent. Load and stress testing is an art unto itself, and it&#8217;s smart to get some people involved who have done it before, and know what to look for.

Once you know where your system will fail under increasing load, you can make an informed decision as to whether or not it&#8217;s production-ready.

### The Build

The **initial** deploy of a system into it&#8217;s production environment is one thing, but being able to achieve something once does not mean you can do it again, reliably, repeatably, and quickly. That&#8217;s what an automated build and deploy mechanism is for. Ideally, such a mechanism would be a part of your continuous integration/continuous delivery mechanism, so that you know your build and deploy works because you do it dozens of times per day. Leaving such an essential step to chance, and testing it only &#8220;for real&#8221; when you release a new version, is a recipe for pain.

Don&#8217;t forget about dependencies: Your system is not just your code, it&#8217;s all the code from the UI to the metal &#8211; if any piece of that totem-pole changes, you must suspect the whole.

### The Architecture

The structure of a system has a lot to do with how easy it will be to test, to deploy, and, critically, to continue to change, fix and maintain for it&#8217;s whole lifecycle. A monolithic pile of spaghetti can be deployed, and might work just fine initially, but will you be able to change it, fix it, extend it and adapt it on an ongoing basis without a continually increasing cost per feature? If not, then your architecture might not be where you want it.

Once all of these aspects have been considered, I think it&#8217;s time to consider a system&#8217;s readiness for production. 

Edit: Thanks to Hubert Behaghel (@behaghel), a new very important concern:

### Monitoring

If your tests give you confidence that your app is working initially, it&#8217;s your monitoring that gives you the **ongoing</p> 
peace of mind that your app **keeps** working. Part of this is basic uptime monitoring, and perhaps something like Monit to restart any failed processes, but deeper solutions such as NewRelic or Statsd/Graphite to get more insight into the activity of your application.

What am I missing? Drop me a line at mnash@jglobal.com
