---
title: Maven with included Dependencies
author: mnash
layout: post
permalink: /maven-with-included-dependencies/
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
  - Tips and Tricks
tags:
  - configuration
  - Java
  - Maven
  - Netbeans
---
One of the most common, and, in my opinion, valid criticism&#8217;s of Apache Maven is the way it handles dependencies.

The default way of doing dependencies in Maven is for a build to look for dependency jars in one of a specified number of places. If you don&#8217;t specify a location, it will start with your local Maven repository, then a stock set of online repositories (such as ibiblio).

What this means is that you can quickly and easily add a dependency to your project by just listing it in the POM, and Maven will frequently just go get it for you as required. For dependencies that don&#8217;t change rapidly (which is generally a bad idea for entirely separate reasons), the local copy is always used, so after the first download you don&#8217;t go get the jar again unless it changes.

The downside of this (and hence the basis for the criticism) is that your local repository is considered a cache, and is not checked in to your source control system. Maven aficionados believe that source control should be for what the name implies: source, not jars (which are an artifact, not source code). This is good, except in situations where the local repository is removed (as it&#8217;s a cache, and not &#8220;backed up&#8221; by being in source control) and you want to rebuild your project. Normally, no problem: Maven will simply go back out into the wilds of the internet and get your jars for you again. Except when it can&#8217;t, which is where the problem starts.

Let&#8217;s say your project depends on foo-1.0.jar, for the sake of discussion. Foo-1.0.jar is found in a repository at http://baz.com. No problem. Two months from now, you come back and make a change to your project, and your local repo doesn&#8217;t have foo-1.0.jar in it. Maven goes to get it for you, but baz.com has gone offline. Oops. Now you can&#8217;t build your project at all. Worse, let&#8217;s say you \*do\* find foo-1.0.jar, but it&#8217;s been updated. Granted, this is a gross violation of the version scheme, but as baz.com is not under your control, it \*can\* happen &#8211; and Murphy was an optimist.

The first level of defense against this is to have a local jar proxy that \*is\* backed up, like Nexus. Nexus not only provides a safe haven for the exact versions of Jars you need to build your project, but also proxies new jars automatically, when set up correctly. That way, once you use that external dependency, it&#8217;s available on the local proxy immediately forever more, in precisely the correct version.

This solution is so good, that I always consider Nexus and Maven to be two parts of one solution &#8211; as you don&#8217;t really have reliable and repeatable builds without Nexus in the mix.

Another way to go, however, is perhaps even more straightforward, and might be appropriate if you have a limited number of &#8220;internal&#8221; binary dependencies &#8211; that is, binary dependencies that you generate within your organization between projects. 

This is the option I want to describe in this blog, and it takes a form very similar to the old Ant style of having a &#8220;lib&#8221; directory in your project, and checking jars into source control.

You simply create a directory (called lib or whatever you wish, but &#8220;lib&#8221; might be more standard), and put your jar dependencies in it. Then you refer to each dependency in your pom.xml file with a special syntax, like so:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
    &lt;dependency&gt;
      &lt;groupId&gt;mygroup&lt;/groupId&gt;
      &lt;artifactId&gt;myjar&lt;/artifactId&gt;
      &lt;version&gt;1.0.0&lt;/version&gt;
      &lt;scope&gt;system&lt;/scope&gt;
      &lt;systemPath&gt;${basedir}/src/main/resources/lib/myjar-1.0.0.jar&lt;/systemPath&gt;
    &lt;/dependency&gt;
&lt;/code&gt;
</pre>
</div>

Now the myjar-1.0.0.jar will be on my classpath during compilation, easy as that. I can then check in that nicely versioned jar file, and have a fully self-contained project, while at the same time being able to leverage the power of Maven and it&#8217;s rich ecosystem of plugins. If you&#8217;re using the shade plugin, this is an excellent way to create a self-contained executable jar file containing all of your necessary dependencies in one shot, rather than having to worry about classpaths at runtime.

In web applications, you can do even better. By placing the dependency in the correct spot in your source tree, you can have it automatically included in the finished .war file, while at the same time finding it in your classpath during compile time, like so:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
    &lt;dependency&gt;
      &lt;groupId&gt;xstream&lt;/groupId&gt;
      &lt;artifactId&gt;xstream&lt;/artifactId&gt;
      &lt;version&gt;1.3.1&lt;/version&gt;
      &lt;scope&gt;system&lt;/scope&gt;
      &lt;systemPath&gt;${basedir}/src/main/webapp/WEB-INF/lib/xstream-1.3.1.jar&lt;/systemPath&gt;
    &lt;/dependency&gt;
&lt;/code&gt;
</pre>
</div>

This includes the xstream jar in my webapp. Every IDE that can digest a POM file (which include my 3 main ones, IntelliJ IDEA, Eclipse IDE and Netbeans) also automagically find the dependencies.

One minor constraint here is that you must use a \*versioned\* jar file &#8211; e.g. it must be named according to the artifact-version.jar pattern. I consider this a feature, not a limitation, as I&#8217;m a firm believer that all artifacts should be properly versioned, so I can tell what source code originally created them. Yes, I know that can be done internally, in a manifest or such, but I like to see the label on the outside of the box, so to speak.

As one colleague put it, now you can be assured of coming back to your project months or years later, even if you don&#8217;t have internet connectivity, and be able to build the darn thing again, without going off on a wild jar chase all over the internet.

This pattern can overcome a serious and legitimate objection to Maven, and might be appropriate in many situations. Give it a try, let me know what you think!