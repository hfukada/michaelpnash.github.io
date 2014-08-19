---
title: Lift in ServiceMix 4
author: mnash
layout: post
permalink: /lift-in-servicemix-4/
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
  - configuration
  - Lift
  - Maven
  - Scala
  - ServiceMix
  - webapps
---
Apache&#8217;s [ServiceMix 4][1] is a unique combination of OSGi container and JBI-compliant ESB, but in addition to this it&#8217;s also a capable web application container. More specifically, it can **contain** a webapp container, but the effect is the same&#8230;

My current favorite tool for cranking out MVC-style webapps is the [Lift framework][2], so I thought I&#8217;d document here the process for deploying a Lift webapp into ServiceMix 4.

The good news is that it&#8217;s very straightforward.

First, build the .war for your Lift app using **mvn package**. This will result in a .war file in the target directory of your project, and is well-covered by the Lift documentation if you need more details. In my case, I started with a slightly modified version of the PocketChange example app for Lift.

Now start servicemix with 

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
bin/servicemix
&lt;/code&gt;
</pre>
</div>

Done from the root directory of your ServiceMix install. You should see the ServiceMix banner after a few moments, followed by a prompt.

In the console, type the &#8220;osgi&#8221; command to enter OSGi mode.  
then

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
install war:file:///tmp/admin-0.1.war?Webapp-Context=admin
&lt;/code&gt;
</pre>
</div>

You&#8217;ll see some startup messages as your webapp is digested by ServiceMix, turned automagically into a bundle, and processed by various intestinal organs such as the HTTP service.

Now surf to 

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;

http://localhost:8080/admin/

&lt;/code&gt;
</pre>
</div>

And up comes your application!!

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

 [1]: http://servicemix.apache.org/SMX4/index.html
 [2]: http://liftweb.net/