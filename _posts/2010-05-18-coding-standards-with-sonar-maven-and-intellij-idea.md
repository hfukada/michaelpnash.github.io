---
title: Coding Standards with Sonar, Maven and Intellij IDEA
author: mnash
layout: post
permalink: /coding-standards-with-sonar-maven-and-intellij-idea/
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
tags:
  - Java
  - Maven
  - quality
  - testing
---
One of the ways to ensure quality in a software project is to find a set of coding standards that your team can agree on then put automated checks in place to ensure they are adhered to.

In this post I&#8217;d like to take a very small example of such a stanard, and show how you can use several different tools to help ensure and measure compliance.

**The Example**  
The simple rule we wil use is the use of curl braces on if statements and similar blocks. Our team reached a concensus that we would always prefer this form

<pre class="brush:java">if (condition) {
   block
}
</pre>

over this

<pre class="brush:java">if (condition)
    block
</pre>

even when there is only one line in the block, where the braces are optional. I&#8217;m in the habit of not doing this, so I kept doing it the wrong way, making code just that little bit harder for the rest of the team to read and maintain.

We have an existing codebase of hundreds of thousands of lines, some of which adhere to this rule, some of which doesn&#8217;t.

First, I wanted to measure adherence to the rule, so I chose the [Sonar][1] quality assurance tool. 

**Sonar**  
Sonar installation is straightforward: [download the distribution][2], unzip it and run one script. Sonar runs as a web application, so you can immediate go to your browser and see the initial page, like so:

![sonar empty Coding Standards with Sonar, Maven and Intellij IDEA][3]

I&#8217;m using Sonar (for now) in it&#8217;s default mode with a bundled Derby database. If I were going to use it more heavily, I could install a separate MySQL database, and run Sonar itself inside a container of my choice (it comes bundled with a basic web container so you can get going right away).

For my machine, I ran 

<pre>bin/macosx-universal-64/sonar.sh console
</pre>

&#8220;Console&#8221; runs Sonar without backgrounding the task. Normally you&#8217;d use &#8220;start&#8221;, which works just like a Unix service, and is suitable for running from an init.d-type script immediately. The first time around, Sonar takes a few moments to fire up, as it creates all it&#8217;s required database tables and populates them with an initial set of data to get your started.

Sonar can measure many hundreds of different metrics, but for the purposes of this simple experiment I only want the one, so I create a custom profile, called &#8220;team&#8221;.

![sonar created team profile Coding Standards with Sonar, Maven and Intellij IDEA][4]

I set this profile to be the default, then click to edit it.

Now I can search for the braces rule in checkstyle by setting filter criteria:

![sonar find braces rule Coding Standards with Sonar, Maven and Intellij IDEA][5]

You can click the rule name to see a description, and to set any optional parameters on the rule.

I activate the rule, and leave it at the default &#8220;Minor&#8221; priority.

If I now return to my profile, I have a link to access the generated checkstyle.xml file, the configuration file that is used by checkstyle to configure its rules. This will be important later on.

Now I can go to my project and analyze it by running &#8220;mvn clean install sonar:sonar&#8221;. With the default configuration, this works only when the build is taking place on the same box that Sonar is running, but it&#8217;s simple to set up a settings.xml file to tell the Sonar plugin where to find the Sonar instance, so you can have a single shared Sonar instance for the whole team. This is covered nicely in the Sonar documentation.

One minor hiccup: The released version of the Sonar plugin for Maven doesn&#8217;t work with Maven version 3 (still in Beta), which I was using. You can build the source version if you need this support, or I&#8217;m guessing it&#8217;ll be released about the time Maven 3 might be.

Now that I&#8217;ve analyzed my project, I can go back into Sonar and see how well I adhered to my rule:

![sonar after analysis Coding Standards with Sonar, Maven and Intellij IDEA][6]

As I see I have a violation, I can drill down and see the violation in context right in the code:

![sonar drilldown to violations Coding Standards with Sonar, Maven and Intellij IDEA][7]

This is handy for checking the state of a rule against an existing codebase, but I&#8217;d like to have more immediate feedback. No problem, I can integrate Sonar into both my IDE and my build process very easily.

**IntelliJ IDEA: Immediate Feedback**

There&#8217;s also a new plugin for IntelliJ IDEA for Sonar. To install, just go to the &#8220;Available&#8221; tab in your plugin configuration within IntelliJ, right-click and select Download and Install. You&#8217;ll have to restart IntelliJ to activate the plugin.

Now you can find the Sonar entry in configuration, and set up a URL to point to your Sonar installation, along with a username and password to log in to Sonar. The default is &#8220;admin/admin&#8221;.

Having done that, I can now see violations directly in my code, as I open each file, like so:

![sonar showing in intellij Coding Standards with Sonar, Maven and Intellij IDEA][8]

In the above, I&#8217;m hovering over the little &#8220;price tag&#8221; annotation in the left gutter to see the message. You can also see the usual IntelliJ &#8220;yellow bar&#8221; on the right side of the screen, which shows the same message.

This lets me know of a rule violation before I even attempt to build, so when I forget my braces, I don&#8217;t have to wait to be chastized, IntelliJ can do it for me immediately <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Coding Standards with Sonar, Maven and Intellij IDEA" class="wp-smiley" title="Coding Standards with Sonar, Maven and Intellij IDEA" /> 

**Maven: Ensuring Conformance**

There is a Maven Checkstyle Plugin that allows us to make a run of checkstyle part of the build process of our project. I configured this plugin in my POM like so:

<pre class="brush:xml" collapse="true">&lt;project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
    &lt;groupId&gt;com.jglobal&lt;/groupId&gt;
    &lt;artifactId&gt;experiment&lt;/artifactId&gt;
    &lt;packaging&gt;jar&lt;/packaging&gt;
    &lt;name&gt;Experiment&lt;/name&gt;
    &lt;version&gt;1.0.0-SNAPSHOT&lt;/version&gt;

    &lt;properties&gt;
        &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
    &lt;/properties&gt;

    &lt;dependencies&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;junit&lt;/groupId&gt;
            &lt;artifactId&gt;junit&lt;/artifactId&gt;
            &lt;version&gt;4.5&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;

    &lt;/dependencies&gt;

    &lt;build&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
                &lt;configuration&gt;
                    &lt;source&gt;1.6&lt;/source&gt;
                    &lt;target&gt;1.6&lt;/target&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-checkstyle-plugin&lt;/artifactId&gt;
                &lt;version&gt;2.5&lt;/version&gt;
                &lt;dependencies&gt;
                    &lt;dependency&gt;
                        &lt;groupId&gt;org.codehaus.plexus&lt;/groupId&gt;
                        &lt;artifactId&gt;plexus-resources&lt;/artifactId&gt;
                        &lt;version&gt;1.0-alpha-7&lt;/version&gt;
                    &lt;/dependency&gt;
                &lt;/dependencies&gt;
                &lt;configuration&gt;
                    &lt;configLocation&gt;http://localhost:9000/rules_configuration/export/java/team/checkstyle.xml
                    &lt;/configLocation&gt;
                    &lt;consoleOutput&gt;true&lt;/consoleOutput&gt;
                    &lt;failsOnError&gt;true&lt;/failsOnError&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.codehaus.sonar&lt;/groupId&gt;
                &lt;artifactId&gt;sonar-maven-plugin&lt;/artifactId&gt;
                &lt;version&gt;1.8M1&lt;/version&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
    &lt;/build&gt;

&lt;pluginRepositories&gt;
        &lt;pluginRepository&gt;
            &lt;id&gt;codehaus&lt;/id&gt;
            &lt;name&gt;Maven Plugin Repository&lt;/name&gt;
            &lt;url&gt;http://repository.codehaus.org/&lt;/url&gt;
            &lt;layout&gt;default&lt;/layout&gt;
            &lt;snapshots&gt;
                &lt;enabled&gt;false&lt;/enabled&gt;
            &lt;/snapshots&gt;
            &lt;releases&gt;
                &lt;updatePolicy&gt;never&lt;/updatePolicy&gt;
            &lt;/releases&gt;
        &lt;/pluginRepository&gt;
    &lt;/pluginRepositories&gt;
&lt;/project&gt;
</pre>

As you can see, instead of providing a file system based location for the configuration file for Checkstyle, I just pointed the Checkstyle plugin at my Sonar-generated checkstyle.xml, this way my IDE, Sonar and my build stay in perfect sync, and I have a nice GUI for adjusting my checkstyle rules, instead of having to hand-edit XML.

Now when I run my build, Maven will analyze my project against the checkstyle rules, and report any violations. With code as we&#8217;ve seen above, it of course reports a violation, but the build still succeeds.

This is fine, but now that I&#8217;ve verified we are adhering to this rule, I&#8217;d like to actually fail the build if we slip back. Also easily done &#8211; in Sonar, I just change the level of violation for my one and only rule to &#8220;Critical&#8221; in my profile. Now when I run my Maven build, sure enough, the build fails, noting the fact that I&#8217;m not adhering to a Critical rule.

As my codebase gets cleaner and cleaner, I can up the priority of the rules I really care about until there are no more violations &#8211; then Maven and Sonar can guarantee it stays that way. Of course, in a multimodule build (e.g. with an aggregator POM), I might want to create a parent POM, and specify all this configuration there. (It&#8217;s generally not a good idea to have the aggregator and the parent in one pom, use two).

This is of course a trivial example of Sonar, IntelliJ and Maven working together. Sonar can apply over 700 rules right out of the box, and more can be added via plugins easily.

What I find good is that I can synchronize all my tools off one common and agreed-upon rulebase, without having to tweak XML files all over the place to gradually increase my quality standards over time.

 [1]: http://www.sonarsource.org/
 [2]: http://www.sonarsource.org/downloads/
 [3]: http://50.116.19.42/wordpress/wp-content/uploads/2010/05/sonar-empty.jpg "Coding Standards with Sonar, Maven and Intellij IDEA"
 [4]: http://50.116.19.42/wordpress/wp-content/uploads/2010/05/sonar-created-team-profile.jpg "Coding Standards with Sonar, Maven and Intellij IDEA"
 [5]: http://50.116.19.42/wordpress/wp-content/uploads/2010/05/sonar-find-braces-rule.jpg "Coding Standards with Sonar, Maven and Intellij IDEA"
 [6]: http://50.116.19.42/wordpress/wp-content/uploads/2010/05/sonar-after-analysis.jpg "Coding Standards with Sonar, Maven and Intellij IDEA"
 [7]: http://50.116.19.42/wordpress/wp-content/uploads/2010/05/sonar-drilldown-to-violations.jpg "Coding Standards with Sonar, Maven and Intellij IDEA"
 [8]: http://50.116.19.42/wordpress/wp-content/uploads/2010/05/sonar-showing-in-intellij.jpg "Coding Standards with Sonar, Maven and Intellij IDEA"