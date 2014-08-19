---
title: 'How it&#8217;s Made: Matrix Decider'
author: mnash
excerpt: "I've recently had an opportunity to build a small project from start to finish, and I thought it would be interesting to document the whole process, from laying the plans to initial release. Also, as much of my work is commercial development, my opportunity to document and share the whole process is limited. In this case, Matrix Decider is open source, so I can tell all :)"
layout: post
permalink: /how-its-made-matrix-decider/
related_exlink_4:
  - 
related_exlink_3_desc:
  - 
related_exlink_3:
  - 
related_exlink_2_desc:
  - 
related_exlink_5:
  - 
related_exlink_4_desc:
  - 
related_exlink_2:
  - 
related_exlink_1:
  - 
related_exlink_1_desc:
  - 
related_exlink_5_desc:
  - 
categories:
  - Scala
  - Software Design
tags:
  - Play
---
I&#8217;ve recently had an opportunity to build a small project from start to finish, and I thought it would be interesting to document the whole process, from laying the plans to initial release. Also, as much of my work is commercial development, my opportunity to document and share the whole process is limited. In this case, [Matrix Decider is open source][1], so I can tell all <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile How its Made: Matrix Decider" class="wp-smiley" title="How its Made: Matrix Decider" /> 

## Product plan

This project had a somewhat lighter plan than many projects I work on, as it was partly an experiment: I wanted to do a small end-to-end application using the [Play framework][2], to gain experience and help cement my understanding of the framework itself. My goal was to have an application that provided an actual (if trivial) set of functionality (and no, I couldn&#8217;t bring myself to do another TODO-list application!), and to have it use all my normal processes and workflows, to see if that presented any issues that needed to be resolved.

I&#8217;ve used the workflow described here many times before, and most of the technologies as well, but there&#8217;s no substitute for going through the whole process.

## DDD

Employing [Domain-Drive design][3] principles, I prepared a [bounded context][4] for this domain that included the following Ubiquitous language:

**Decision**: A set of alternatives and criteria that can be combined in a logical way to determine an optimal choice from amongst the alternatives. An example might be &#8220;Choose a Car to Buy&#8221;  
**Alternative**: One of the choices among which a decision is to be made. For example, Ford Focus Model XYZ, Honda Accord, Range Rover  
**Criteria**: A way to evaluate the desirability of a specific alternative, for example: price, fuel efficiency, color. A criteria may be assigned a relative Importance, e.g. &#8220;trivial&#8221;, &#8220;critical&#8221;, &#8220;very important&#8221;, etc.  
**Ranking**: The rating of a specific alternative with respect to a criteria.  
**User**: An individual who may have zero or more decisions in progress at any given time.

Within this context we have several entities and one aggregate. User is an entity. Decision is the aggregate, and alternatives and criteria are accessed via the decision aggregate root.

## Pivotal Tracker

As soon as the domain was designed, I began story breakdown in [Pivotal Tracker][5], my tool of choice for planning and managing projects. I&#8217;ve used many others, but they are all much heavier in weight and provide me no additional value. I created a number of stories in a backlog, ordered by priority and dependency (e.g. where one story can&#8217;t be done until some other story is completed).

## Technology Choices

What I selected and why.

### Play!

As part of the plan here was to give a good workout to the [Play framework][2], it was the centrepiece of this application. Plenty has been written about it, so suffice it to say that it was a very efficient and pleasant development experience, and I&#8217;ll be using it a lot more in the future. I use the Scala version of Play, as Scala is my go-to language, for reasons that require another entire blog post to discuss.

### Slick

I wanted a very lightweight persistence layer, and my choices ran between using [MongoDB][6], and persisting on a database hosted at [MongoHQ][7], or [Hypersonic][8], both of which I&#8217;ve used many times before. Using [Slick][9], the difference in implementation between the two was not that large, but HSQL did have the advantage of having an in-memory mode for easy testing. And yes, I know and have used [Fongo][10], but it&#8217;s not quite as lightweight in most situations.

### HSQL

I&#8217;ve used [Hypersonic][8] for many years, and it&#8217;s gotten more capable and valuable to me over time. As I specifically wanted a relational model for Matrix-Decider, it was an obvious choice. My implementation allows me to run HSQL in &#8220;in-process/in-memory&#8221; mode for testing and simple deployments, and to easily turn on &#8220;file mode&#8221; without needing to deploy an external server. If I wanted multiple nodes of Matrix Decider working against a single data store (for high availability or to scale out), I could easily do so, although the deployment and monitoring gets a bit more complex, as then I&#8217;d have to deploy Hypersonic in server mode separate from the application itself.

### Cloudbees Jenkins

The company [Cloudbeees][11] offers excellent PaaS for Java applications, not just for execution, but for development as well. I have been using them (as well as a local &#8220;backup&#8221; Jenkins server) for quite a while now, so they were a clear choice. I use [Jenkins][12] (the non-Oracle version of Hudson), for it&#8217;s lightweight yet capable support of continuous integration.

### Monitoring

I use [Monit][13], an excellent tool, to ensure all my applications are up and running as expected, and to restart them in the event of a failure, notifying me via email in that event. In this case, Monit is running on the same Linode instance where I deploy the application itself.

Who watches the watchers? It is of course quite possible for my entire Linode instance to go down &#8211; it doesn&#8217;t happen very often, but there was one brief interruption a while back. What good is my monit then, as it&#8217;s running on the same box? None, of course &#8211; so I have a periodic Jenkins job on my build server ping the box as a double-check. If it doesn&#8217;t get a reply from a known URL, it emails me, and again I know something is up. If alls well, then alls quiet.

## Development Toolset and Environment

Some of the development toolset gets implied by the above technology choices: SBT as my build tool, as that&#8217;s what Play uses in any case, and I&#8217;d prefer it even if it didn&#8217;t.

IDE choice is a subject I&#8217;ve blogged quite a bit about lately, and fortunately the Scala world has plenty of good choices, from the Eclipse plugin to IntelliJ, and many others. I go back and forth a bit, alternating between using IntelliJ IDE and it&#8217;s excellent Scala plugin and using Emacs and Ensime. I&#8217;ve already blogged about my experiments between these two, but no matter which I chose, I used the same engine to drive them.

My specific hardware is a bit more complex, as it&#8217;s not one machine, it&#8217;s many, depending on where I am: When I&#8217;m mobile, I use a MacBook air, but whenever I can I add an external monitor and keyboard. At home I use a Mac Pro much of the time, but in neither case is that what I&#8217;m actually developing on &#8211; both are just used as a front-end to an [Amazon EC2][14] instance. When I&#8217;m using [Emacs][15] I prefer console-based emacs in an [iTerm2][16] terminal window, and using [tmux][17] to manage sessions, allowing me to easily work for a few minutes, drop the connection, switch machines, and resume exactly where I left off. Of course, when I&#8217;m using [IntelliJ][18] I can do much the same, using [X11][19] and the excellent [No-Machine Player][20] for my client.

For that matter, if you want to really go lightweight, you can [develop on an iPad][21], using [iSSH][22] and an external keyboard. I&#8217;ve tried it &#8211; it works!

My EC2 instance is heavy on compute power (20ECUs), medium on memory (8GB), and medium on I/O performance (backed by an EBS instance when the instance is stopped). This gives me the equivilant of a pretty potent development box, but let&#8217;s me access it from anywhere &#8211; or anywhere with a network, which is almost anywhere. For the rare times when I&#8217;m offline entirely, I can still develop quite nicely on the Air standalone, I&#8217;m just not able to compile as fast as I&#8217;m able on the VM.

In either case, I commit very frequently and push to a development branch, ensuring that even if something nasty happens, I won&#8217;t lose more than a few minutes work.

### Continuous Deployment

I have an account with the excellent Cloudbees service, as described above, and although in this case my git repo is on Github, Cloudbees has no problem polling my git repo periodically for changes, and building my app. I build the application using the &#8220;dist&#8221; command in Play, which produces a ready-to-go .zip file. Then I have another job (triggered by the completion of the first) that deploys that zip to the proper location on my Linode server, and shutdown and restart the application.

This is a little more complex than it sounds: first the script must tell Monit to not restart the app for a moment, then bring up the new version. If this works, tell Monit to start watching again, and do the same thing to the other node. This guards against a bad deploy in that if the app won&#8217;t come up or otherwise fails to deploy, only one node is down, and I get an immediate alert.

I use a software load-balancer ([Pound][23]) to keep requests shared across multiple instances of the same application running on one host, in this case. In a full production situation, I&#8217;d use at least a couple of hosts &#8211; ideally in different data centers.

This deploy process happens just about immediately when I check in a change to the application, assuming all tests are still passing.

### TDD

Speaking of tests, I always employ a test-first approach, ensuring that I write code that is easy to test, and that I don&#8217;t write code I don&#8217;t need. Play makes this quite easy.

### Documentation

Much as I believe that code should be self-documenting, that only covers the code itself, not the whole project. To this end, I&#8217;ve prepared s short writeup, in the form of a README for Github, that describes what Matrix Decider is all about, and how to get it and use it.

This post is another form of documentation, albeit not one I usually do for a project.

### Summary

All in all, this was a typical project for me, and held no real surprises. I was able to work with some of the portions of Play that I hadn&#8217;t had the chance to before, and it turns out that the framework does indeed fit my typical project flow, including the ability to test extensively and to deploy continuously.

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

 [1]: https://github.com/michaelpnash/matrix-decider
 [2]: http://www.playframework.com/
 [3]: http://en.wikipedia.org/wiki/Domain-driven_design
 [4]: http://en.wikipedia.org/wiki/Domain-driven_design#Bounded_context
 [5]: https://www.pivotaltracker.com/
 [6]: http://www.mongodb.org/
 [7]: https://www.mongohq.com/home
 [8]: http://hsqldb.org/
 [9]: http://slick.typesafe.com/
 [10]: https://github.com/foursquare/fongo
 [11]: http://www.cloudbees.com/
 [12]: http://jenkins-ci.org/
 [13]: http://mmonit.com/monit/
 [14]: http://aws.amazon.com/ec2/
 [15]: http://www.gnu.org/software/emacs/
 [16]: http://www.iterm2.com/
 [17]: http://tmux.sourceforge.net/
 [18]: http://www.jetbrains.com/idea/
 [19]: http://www.x.org/wiki/
 [20]: http://www.nomachine.com/products.php
 [21]: http://yieldthought.com/post/12239282034/swapped-my-macbook-for-an-ipad
 [22]: https://itunes.apple.com/ca/app/issh-ssh-vnc-console/id287765826?mt=8
 [23]: http://www.apsis.ch/pound