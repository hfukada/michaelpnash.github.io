---
title: 'High Ceremony doesn&#8217;t have to mean High Cycle Time'
author: mnash
layout: post
permalink: /high-ceremony-doesnt-have-to-mean-high-cycle-time/
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
  - Software Testing
  - Tips and Tricks
tags:
  - container
  - cycle
  - high ceremony
  - hot deploy
  - jetty
  - low ceremony
  - Maven
  - python
  - ruby
---
Oftentimes languages such as Java are called &#8220;high ceremony&#8221; languages compared to languages like Ruby or Python. This refers to the fact that there&#8217;s generally a bit more plumbing involved in firing up a Java application &#8211; particularly a web application &#8211; than there is with the scripting languages.

Of course, Java is compiled (to byte-code at least), so it&#8217;s not quite a 1 to 1 comparison with a more interpreted language such as Ruby, but still, even in a &#8220;high ceremony&#8221; language it&#8217;s important not to get too high a &#8220;cycle time&#8221; for developers, IMO.

By &#8220;cycle time&#8221; I mean the time between making a change and seeing it working &#8211; either in a test, or, ideally, in a running application. Most modern IDEs made the cycle time for tests pretty darn low (and great tools like Inifinitest can take all the manual work out of it, no less), but to see a running application and be able to excercise your changes deployed in a container is a bit more of a grind.

That&#8217;s where a tool like [Jetty][1] can come in handy. Jetty is a lightweight web app container that can be easily added to your development cycle in place of a heavier-weight solution to allow you a faster cycle time, and, often, greater productivity and interactivity.

Especially in combination with it&#8217;s integration with [Maven][2], Jetty can get your app deployed far faster than with other solutions. For most webapps, it&#8217;s just a matter of saying:

`mvn jetty:run`

And you&#8217;ve got a container up and running with your app in it within a few seconds.

Jetty can even do a certain amount of &#8220;hot update&#8221;: modify a JSP (or even some code &#8211; although there are limits) and the running webapp is updated, and you&#8217;re able to test, edit&#8230; cycle away without the painful wait for a deployment any more often than necessary.

You can pass required system properties to your app via maven&#8217;s -D mechanism, and they&#8217;ll be available to your app:

`mvn -Dsome.property=someValue jetty:run`

And even control the port your application binds to on the fly (or via the handy jetty.xml file if you want to set it more permanently). 

Jetty and maven also give you the ability to script, for example, if you need to run a test utility on your running webapp to ping a series of REST calls, for example, you can:

`mvn clean package # Build the webapp<br />
mvn jetty:run &#038; # start jetty, spawning it in the background<br />
java -jar mytestutility.jar # Run my test jar, which pings the URLs for all my rest services, maybe does performance checks, etc<br />
mvn jetty:stop # Stop the jetty instance we fired up in the background`

Lightweight containers such as Jetty are just one way to help crank down the &#8220;cycle time&#8221; for developers, of course. Some other possibilities I&#8217;ll leave for a later entry.

 [1]: http://www.mortbay.org/jetty/
 [2]: http://maven.apache.org/