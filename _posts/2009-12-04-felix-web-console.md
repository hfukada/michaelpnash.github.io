---
title: Felix Web Console
author: mnash
layout: post
permalink: /felix-web-console/
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
  - OSGi
  - Software Design
tags:
  - Java
  - open source
  - OSGi
  - ServiceMix
---
In my ongoing experiments with Apache ServiceMix, I recently installed the [Felix Web Console project][1], and it was simple and helpful.

OSGi containers typically have a &#8220;console&#8221; for administering the bundles you&#8217;re deploying into our container via the command-line. ServiceMix has a nice &#8220;remote&#8221; feature, that allows me to get to the console of our ServiceMix instance from my local machine easily, without having to actually ssh to the ServiceMix box.

It looks like this:

![osgi command line console Felix Web Console][2]

You can list your bundles, install, uninstall, restart, etc, all from here.

What Felix Web Console brings to the table is a nice webapp front-end on all this functionality.

Installation is the easiest thing possible: you go to your existing console and type:

<div class="capsule" style="text-align: left">
  <pre>
 &lt;code&gt;
   &lt;dependency&gt;
smx@root:osgi&gt; install http://mirror.switch.ch/mirror/apache/dist/felix/org.apache.felix.webconsole-2.0.2.jar
&lt;/code&gt;
</pre>
</div>

It reports that a new bundle is installed, and gives you the number (237 in my case).

Then I say:

<div class="capsule" style="text-align: left">
  <pre>
 &lt;code&gt;
start 237
&lt;/code&gt;
</pre>
</div>

And I can immediately surf to the following URL in my browser: http://servicemix.point2.com:8080/system/console

and see the following page:

![felix web console bundles Felix Web Console][3]

Now I can browse my bundles, install, uninstall &#8211; and all the same good stuff as via the console, even view the output of the log service, except all from the comfort of my web browser.

Like many things in the OSGi world, it just works like it&#8217;s supposed to, and is much easier to do than it is to explain <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Felix Web Console" class="wp-smiley" title="Felix Web Console" />

 [1]: http://felix.apache.org/site/apache-felix-web-console.html)
 [2]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/osgi-command-line-console.jpg "Felix Web Console"
 [3]: http://50.116.19.42/wordpress/wp-content/uploads/2009/11/felix-web-console-bundles.jpg "Felix Web Console"