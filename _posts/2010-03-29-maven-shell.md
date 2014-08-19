---
title: Maven Shell
author: mnash
layout: post
permalink: /maven-shell/
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
  - Software Design
---
If you work with [Apache Maven][1] at all, you&#8217;ve probably checked out the still-unreleased alpha&#8217;s of Maven 3. I&#8217;ve been working with the alpha-6 for a number of weeks, and I&#8217;ve found it solid and reliable, with no changes required to my pre-maven-3 pom file at all.

The only noticeable change is that it&#8217;s less chatty to the console, and it runs about 30% faster than before. 

I did fall down one hole, but it was a short-lived problem: I was doing something that is arguably not too smart in the first place &#8211; that is, calling my &#8220;deploy&#8221; script on local workstations using a binding to a Maven lifecycle and using the Ant plugin. It turns out the point at which I&#8217;d bind to the lifecycle wasn&#8217;t well-defined, and Maven 3 had different behaviour in this area than Maven 2. The fix was easy: don&#8217;t do that :). I now simply call my ant deploy script manually at the end of the build cycle, using the unix &#8220;&#038;&#038;&#8221; command, so it only runs if the build succeeded (as I don&#8217;t want to deploy the old code if the build of the new didn&#8217;t work).

On top of the speed boost I&#8217;ve seen with Maven 3, I also tried the very-alpha [Maven Shell][2] project, hosted at Sonatype. 

This project basically gives you a shell, much like a unix/linux shell, but that is &#8220;Maven Aware&#8221;. You type your Maven commands just like before, e.g. &#8220;mvn clean install&#8221;, but the Maven Shell already has an instance of Maven loaded, so execution begins faster, and it caches POMs and such, so the runtime even beyond startup is faster still. I was able to take a 2+ minute build cycle (on an old, tired laptop) and take it down to 30 seconds, by using both Maven 3 and the Maven Shell. 

Not bad, not bad at all.

 [1]: http://maven.apache.org/
 [2]: http://mvnsh.sonatype.org/