---
title: Look Ma, No Container!
author: mnash
excerpt: "Your webapps don't need a container, and might be better off without one"
layout: post
permalink: /look-ma-no-container/
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
---
Recently I&#8217;ve been working on a number of projects that deploy Scala web applications to Tomcat, our container of choice. 

Now, I&#8217;ve been using Tomcat for a long time, and it&#8217;s always done a pretty good job for me. One quirk that has always existed, in one way or another, was that it is occasionally necessary to restart Tomcat, no matter how well-behaved and non-leaking my applications are. You can make this quite seldom with carefully tuned memory arguments to your JVM, especially including the options that allow garbage-collection and re-use of permgen space, but I&#8217;ve never been able to simply make it unnecessary to eventually restart Tomcat.

Sometimes, Tomcat will even go down &#8220;hard&#8221;, becoming unresponsive and unable to be killed through it&#8217;s normal admin process, which is even worse, as this makes automated redeployment unreliable and slow.

I don&#8217;t think any of this is particular to Tomcat, either &#8211; I&#8217;ve seen variations on the same kind of issues with a great many Java servlet containers over the years, to a lesser (Jetty) and greater (Weblogic) degree.

In the last while, I&#8217;ve been developing web service applications based on the excellent [Akka][1] framework, and [Spray][2] on top of it. Spray has recently added a very thin container replacement called &#8220;Spray-Can&#8221;, which you can read about in detail on the Spray site. 

In combination with the <abref="https://github.com/eed3si9n/sbt-assembly">SBT &#8220;assembly&#8221; plugin</a>, I&#8217;ve found it&#8217;s possible to deploy my apps in an entirely different way. Although there is, technically, still a container, it feels quite containerless in practice.

I build my application into a single executable JAR file, as opposed to the .war format so familiar to Java developers.

When this jar is run, my application becomes available on the configured port (8080 by default, but whatever I set it to, even at runtime).

This allows me to create a very simple script to keep my app running at all times, and to easily facilitate downtime-free upgrades, even on a single machine. Let me detail this&#8230;

My /etc/init.d script simply runs my executable jar file in a loop: e.g. something like this:

<pre>while true
do
  java -jar /apps/dir/myapp*.jar
done
</pre>

Then I place the initial version, say 1.0, in the /apps/dir and run my script. Up pops my app.

Now I have another /etc/init.d start a second copy of the app, either on the same machine on a different port or on a second machine entirely. (I&#8217;ve found the lower memory requirements of this allow at least 3 copies on a single machine, though, compared with a full container). 

Now I use something like Apache with mod\_rewrite/mod\_proxy, or balance or, my personal favorite, pound on the front end, so the concern of where my app is visible as far as URLs is entirely removed from the app itself. The application itself comes up on the context root &#8220;/&#8221;, on, say, port 8080 and 8081. Then my pound config simply redirects URLs of the form /url/to/app to one of these two ports, with failover/load balancing. My app neither knows nor cares it&#8217;s on the URL /url/to/app, that&#8217;s pound&#8217;s concern. It can even be behind HTTPS for all it cares &#8211; pound (or apache) takes care of that too.

Now when I want to deploy, I simply copy a new jar into the proper location in /apps/dir, e.g. myapp-2.0.jar.

Now I send a &#8220;poison pill&#8221; to my app in the form of a URL that causes it to shut down. My pound router filters out this call from outside the local network, so client&#8217;s can&#8217;t send it, and I send it directly to the running app (e.g. on port 8080 or 8081). This causes the app to terminate and exit completely, cleaning up any connections it needs to on the way. The VM terminates, and the shell script immediately starts up the new version on the same port.

All this time the second node on 8081 is still going strong with the old version, of course, so the clients never notice the bump.

Now I do the same to node two. When I say &#8220;I&#8221; here, I&#8217;m of course referring to my trusty Jenkins server, which is doing all this for me automatically.

Now I have all of the advantages of my app, in a highly cluster-able lightweight fashion, without using a servlet container at all.

I used to do something similar with the lightweight winstone server (which Jenkins itself uses, incidentally), but for Spray apps, the servlet API is something I don&#8217;t need, and I can run a much higher performance multi-core Akka stack instead, with all the same &#8220;containerless&#8221; advantages.

I recommend you have a look!

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

 [1]: http://akka.io
 [2]: http://spray.cc