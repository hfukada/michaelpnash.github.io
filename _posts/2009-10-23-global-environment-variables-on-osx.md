---
title: Global Environment Variables on OSX
author: mnash
layout: post
permalink: /global-environment-variables-on-osx/
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
I had a situation yesterday where I needed to have the value of an environment variable visible within my IDE, which currently happens to be IntelliJ IDEA. My operating system for this environment is OSX (on a Mac), so my first instinct was to set the variable in my .profile.

This works fine for applications I launch from a Terminal window using the shell &#8211; such as Maven or Ant. 

Unfortunately, IntelliJ didn&#8217;t &#8220;see&#8221; the variable at all, as it&#8217;s launched as a regular Mac application (from my Toolbar or as an application in the Applications folder). As I was accessing the variable from within a Maven POM file within IntelliJ, it was polite enough to highlight it in red. The same POM file worked fine from the command-line, but of course that&#8217;s because the variable was being set within my .profile, so the shell could &#8220;see&#8221; it.

My second instinct was to put it in /etc/profile, in the *nix fashion, but this didn&#8217;t work either.

A bit of googling found the answer, though. I created a file called &#8220;launchd.conf&#8221; in the /etc directory. (You&#8217;ll need to use &#8220;sudo&#8221; to edit this file, e.g. &#8220;sudo vi /etc/launchd.conf&#8221;)

In this file I can add &#8220;setenv&#8221; commands to establish values for the environment variables I need. In this case, I needed to specify a variable to tell my Maven build files (which I use from inside IntelliJ) where my Weblogic installation resides, so I did:

`<br />
setenv WL_HOME /Users/mnash/bea/wlserver_10.3<br />
`

Then I reboot, and voila, my variable value is now available both from a command window **and** from within IntelliJ.

Thought I&#8217;d pass this along.

My thanks to [this article][1] for the information about launchd.conf.

 [1]: http://www.digitaledgesw.com/node/31