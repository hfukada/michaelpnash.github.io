---
title: 'Tales from Vegas, Part 1: James Gosling Keynote'
author: mnash
layout: post
permalink: /tales-from-vegas-part-1-james-gosling-keynote/
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
  - Java
  - News
  - OSGi
  - Review
tags:
  - Java
  - OSGi
  - TSSJS
---
A few weeks ago I had an opportunity to go to The Server-Side Java Symposium, an annual event for Java aficionados held in Las Vegas, Nevada. What happened there will not stay there, however.

I found a few interesting things out, and I&#8217;m going to try to share them over the course of a few blog posts, in case anyone out there is interested, and so I can find them later for myself as well <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Tales from Vegas, Part 1: James Gosling Keynote" class="wp-smiley" title="Tales from Vegas, Part 1: James Gosling Keynote" /> 

TSSJS is not about vendors, it&#8217;s about technical info, so there were only a few &#8220;booths&#8221; from the handful of commercial sponsors of the event, one of which was, inevitably, Oracle. Given the Sun acquisition, a question on the mind of many developers has been &#8220;what&#8217;s Oracle going to do for/with/to Java?&#8221;.

It&#8217;s a legitimate concern, and indeed a complex question with a number of complex answers &#8211; but one of my reasons for being in Vegas was to get some of the answers.

The keynote presentation at TSSJS was by James Gosling, the &#8220;father&#8221; of Java. As everyone no doubt reading this already knows, he&#8217;s subsequently left Oracle, for undisclosed reasons. That, to me, lessens the impact of his remarks somewhat, as I suspect he knew by the time we heard him speak in Vegas that he&#8217;d be on the way out the door, but he still had a lot of interesting things to say.

About 800 people were in the room, I estimated, to hear the keynote. Interestingly enough, Gosling&#8217;s position at Oracle was &#8220;Client Software Group&#8221; VP. I generally don&#8217;t think of Java as having much to do with &#8220;client&#8221; software, personally, so that in itself was informative.

He had an image of the Java mascot (the little delta-shaped guy) wearing a snorkle in a fish tank, a play on the &#8220;Soracle&#8221; name mash-up.

In any case, the keynote touched on what&#8217;s happening in the Java world. He emphasized the wide spectrum of devices on which Java is found, and how networking ties all of these devices more and more into a cohesive whole.

Some stats were mentioned: there are about 15 million downloads per week of Java, and something like 10 billion (with a &#8220;B&#8221;) Java-enabled devices of one sort or another out there in the wild, perhaps 1 billion of which are Java-enabled desktops. By any metric, Java is a huge success, and is in many ways more popular in the rest of the world, especially Europe, than it is in North America.

100 million of those devices are are TV devices, and on top of all it are about 2.6 billion Java-enabled cell phones. 

Conclusion: It&#8217;s not going away, soon or quickly <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Tales from Vegas, Part 1: James Gosling Keynote" class="wp-smiley" title="Tales from Vegas, Part 1: James Gosling Keynote" /> 

A site like the Apple App Store existed for Java apps 7 years before Apple&#8217;s app store &#8211; but it was in Japan.

There are 5.5 billion smart card devices Java-enabled out there &#8211; the V3 standard actually has a servlet container in it &#8211; U.S. military dog-tags apparently now use this standard.

The Amazon Kindle is a Java device, under the skin.

Gosling proffered a definition of success: being completely invisible, people just get stuff done.

There are something like 6.5 million professional Java developers out there, 800 thousand of which are in India. Most colleges have a Java course requirement, modifying the old saw of &#8220;write once, run anywhere&#8221; to include &#8220;learn once, work anywhere&#8221;.

After this deluge of interesting stats, Gosling moved on to discuss the next big thing in Java, in his opinion: Java EE 6, the foundation for next-generation enterprise software. The spec was approved November 30th, 2009.

There are two major flavors of JEE6 &#8211; the &#8220;full&#8221; profile, with everything, and the &#8220;web&#8221; profile, with EJB3 &#8220;Lite&#8221; and just the most frequently used specs, not the more obscure stuff.

A major emphasis in next-generation Java development is modularity: making hard problems easier by breaking them into a number of less-hard problems. Major endorsement here for OSGi.

As far as Gosling&#8217;s concerned, the correct amount of XML required is exactly none <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Tales from Vegas, Part 1: James Gosling Keynote" class="wp-smiley" title="Tales from Vegas, Part 1: James Gosling Keynote" /> Many developers in the room agreed with him, and it&#8217;s now possible with JEE6 and it&#8217;s powerful annotations.

Much of the benefit of dependency injection and resolution that Spring provides has been baking into the core Java EE platform now, and much of the pain of EJB has gone away. In fact, one of the **most** painful parts of EJBs, CMP Entity Beans, is no longer supported by the spec at all, in favor of JPA.

Glassfish V3 is the JEE6 reference implementation, and it&#8217;s OSGi-based.

Then it was demo time: Gosling (with some help from a couple of developer types) fired up Netbeans and Glassfish and did some show and tell of the coolness of JEE6.

We saw a webapp deployed &#8211; with no web.xml, no WEB-INF directory at all, everything annotation-based and dependency-injected at the proper times. We saw a stateless EJB auto-deployed to via an OSGi bundle into the container in less than a second, direct from the IDE. No boilerplate, no config, no reams of XML files to bolt it all together, just code and go.

We saw that same app preserve session state even when it was redeployed, which was very cool (a counter was showing the number of hits to the page &#8211; code was changed and redeployed, and the counter kept incrementing &#8211; and no, it wasn&#8217;t stored in a client-side cookie, it was in the session).

I noticed that all the Oracle guys were using Macs, incidentally <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Tales from Vegas, Part 1: James Gosling Keynote" class="wp-smiley" title="Tales from Vegas, Part 1: James Gosling Keynote" /> 

Gosling notes that JEE6 shouldn&#8217;t just be one version number past JEE5 &#8211; it&#8217;s more like JEE 60 in comparison <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Tales from Vegas, Part 1: James Gosling Keynote" class="wp-smiley" title="Tales from Vegas, Part 1: James Gosling Keynote" /> 

Saw the @Schedule annotation, where a bean can be scheduled for execution with cron-like ease, but all within a JVM.

Gosling noted that Felix was the web container under the skin of Glassfish.

We saw the @Observes annotation being used &#8211; a way to register listeners without any code or configuration. It was noted that Swing could benefit enormously by this pattern.

Then we saw a demonstration of Glassfish&#8217;s web console. The &#8220;web profile&#8221; of JEE6 doesn&#8217;t include JMS by default, so the example shown was adding that support by installing a new bundle in the running container. Two clicks and it was done. A GUI admin console can be added for any bundle, including your own bundles.

Gosling then wrapped up with an overview of some of his personal projects, and then took some questions. He also mentioned a new &#8220;app store&#8221; for Java that&#8217;s in the works, to be coming on &#8220;store.java.com&#8221;. It&#8217;s in the final stages of work now, apparently.

That was the end of the first keynote of TSSJS. In the next few posts I&#8217;ll talk about some additional sessions that my associate and I attended, and some of the other good stuff we learned.