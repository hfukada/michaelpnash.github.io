---
title: RAD with Scala and Vaadin
author: mnash
excerpt: Rapid application development with Scala and Vaadin
layout: post
permalink: /rad-with-scala-and-vaadin/
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
tags:
  - deploy
  - Maven
  - OSGi
  - RAD
  - Scala
  - Vaadin
  - webapps
---
I&#8217;ve had an opportunity recently to work on a product that needed an RIA web interface, and I chose my recent favorite tool for this, [Vaadin][1]. The services for this project needed to be highly scalable, and lent themselves well to functional techniques, so I selected [Scala][2] as my language of choice. I build my projects with Maven, for reasons I won&#8217;t go into right now, and I do much of my JVM-language work in Intellij&#8217;s excellent IDEA IDE.

Given these tools, I found a way to facilitate very rapid development of web UI&#8217;s, and I thought I&#8217;d pass it along.

Another technique I use, which I&#8217;ll expound on later, is creating &#8220;dummy&#8221; implementations of all of my backing services for my application. The &#8220;real&#8221; implementations are written as OSGi services, in separate modules from my UI. The UI is packaged as a war, but is also OSGi aware, with a bundle activator. This activator only gets called if the war is deployed into an OSGi container, and not otherwise. This allows the app to select which implementation of the services it uses &#8211; the &#8220;dummy&#8221; ones when it&#8217;s deployed outside of OSGi, and the &#8220;real&#8221; ones when they&#8217;re available.

This means I can use the handy [Maven jetty plugin][3] to quickly spin up my application and test it on my local workstation, without needing all of the dependencies (like a data store and such) of my real services. That&#8217;s good, in that I can get my &#8220;cycle time&#8221; down to a few seconds, where &#8220;cycle time&#8221; is the time between making a change and actually being able to test it in my browser.

We can do better, though.

I&#8217;m using Scala as my language of choice for building the UI as well, as it works just fine with Vaadin (and with everything else in the JVM ecosystem, for that matter, which is why I didn&#8217;t choose a non-JVM language &#8211; but that&#8217;s yet another rant).

I compile my Scala with the [Maven scala plugin][4] &#8211; here&#8217;s where the next handy bit comes into play. Turns out the Scala plugin has a [goal called &#8220;cc&#8221;][5], for continuous compilation. Using this, I can fire up Maven with a &#8220;mvn scala:cc&#8221; command, and leave it running. Then I also use the &#8220;mvn jetty:run&#8221; command in another window to fire up the web application, and leave it running as well.

Here&#8217;s my configuration for the Scala plugin:

<pre class="brush:xml">&lt;plugin&gt;
                &lt;groupId&gt;org.scala-tools&lt;/groupId&gt;
                &lt;artifactId&gt;maven-scala-plugin&lt;/artifactId&gt;
                &lt;version&gt;2.9.1&lt;/version&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;compile&lt;/goal&gt;
                            &lt;goal&gt;testCompile&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
                &lt;configuration&gt;
                    &lt;scalaVersion&gt;${scala.version}&lt;/scalaVersion&gt;
                    &lt;args&gt;
                        &lt;arg&gt;-target:jvm-1.5&lt;/arg&gt;
                    &lt;/args&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
</pre>

And for Jetty:

<pre class="brush:xml">&lt;plugin&gt;
                &lt;groupId&gt;org.mortbay.jetty&lt;/groupId&gt;
                &lt;artifactId&gt;maven-jetty-plugin&lt;/artifactId&gt;
                &lt;version&gt;6.1.9&lt;/version&gt;
                &lt;configuration&gt;
                    &lt;scanIntervalSeconds&gt;10&lt;/scanIntervalSeconds&gt;
                    &lt;webAppSourceDirectory&gt;src/main/webapp&lt;/webAppSourceDirectory&gt;
                    &lt;jettyConfig&gt;jetty.xml&lt;/jettyConfig&gt;
                    &lt;userRealms&gt;
                        &lt;userRealm implementation="org.mortbay.jetty.security.HashUserRealm"&gt;
                            &lt;name&gt;file&lt;/name&gt;
                            &lt;config&gt;realm.properties&lt;/config&gt;
                        &lt;/userRealm&gt;
                    &lt;/userRealms&gt;
                    &lt;stopKey&gt;stop&lt;/stopKey&gt;
                    &lt;stopPort&gt;8889&lt;/stopPort&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
</pre>

Now I go back to my IntelliJ and start coding. Every time IntelliJ saves (which it does automatically unless you tell it not to), the Scala plugin compiles the files. This generates a new .class file, which the Jetty plugin (well, technically, Jetty itself) detects, and in response, reloads the running classes for the web application.

Net effect is that I can make my change and by the time I switch back to the browser, my new code is running. I test my change, emit the appropriate profanity, and go back to editing, all within a second or two.

This has profound effects on how you develop a UI, which every dynamic language aficionado knows (e.g. like Ruby/Rails or Python/Django). You don&#8217;t hesitate to experiment, and you get to see the visual effect of your changes right away. The good news is that I get to do this with my language of choice, and with all the power of the JVM ecosystem to support it.

The technique is not perfect &#8211; I&#8217;ve found that if you edit some resources or webapp files (images and such), it&#8217;s possible the Jetty plugin doesn&#8217;t &#8220;see&#8221; the change. Of course, two things help with that considerably: first, it&#8217;s lightning-fast to just Control-C the jetty plugin task and re-launch it, and second a Vaadin app generally doesn&#8217;t use many resources, unlike JSP or many other frameworks that make extensive use of templates. 

Once in a while I&#8217;ve found the scala:cc task will report that it&#8217;s lost it&#8217;s connection to the &#8220;fsc&#8221; (fast scala compiler) background process &#8211; again, quickly control-c-ing the task and starting it again solves the problem every time.

Overall, I can crank UI out pretty darn quick with this method, and given that I can TDD even my UI code using Vaadin, I find the overall combination very effective and efficient.

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

 [1]: http://vaadin.com/home
 [2]: http://www.scala-lang.org/
 [3]: http://docs.codehaus.org/display/JETTY/Maven+Jetty+Plugin
 [4]: http://scala-tools.org/mvnsites/maven-scala-plugin/
 [5]: http://scala-tools.org/mvnsites/maven-scala-plugin/cc-mojo.html