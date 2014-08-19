---
title: Automatic Dependency Management with Maven
author: mnash
layout: post
permalink: /automatic-dependency-management-with-maven/
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
  - Software Testing
  - Tips and Tricks
tags:
  - Agile
  - automation
  - components
  - dependencies
  - Java
  - Maven
  - modules
  - testing
---
Apache Maven is a lot more than a &#8220;build tool&#8221;, and one of it&#8217;s major strengths is it&#8217;s ability to manage dependencies.

Maven&#8217;s not just for external dependency management, though &#8211; it can help us work faster and more easily with our own modules as well as those written by others. In fact, it&#8217;s &#8220;internal&#8221; dependency management is actually far more powerful for most development shops.

Every dependency Maven manages is identified with 3 pieces of information &#8211; it&#8217;s group id, it&#8217;s artifact id, and it&#8217;s version. Group id is often some sub-domain of the company it&#8217;s working on, e.g. com.point2.somemodule, and the artifact id helps identify the specific module with that group, like rest-api or such.

Possibly the most interesting part is the version number, though, as this is where the real power of Maven comes to the fore. Versions allow us to maximize the opportunity for parallel development without descending into unversioned chaos. Each version represents a specific point in time in a library&#8217;s development &#8211; and, most importantly, allows us to &#8220;re-assemble&#8221; our application to a known state at any time (not re-build it).

Let&#8217;s take a for-instance to see how this might work&#8230;

**Component-Based Application &#8220;Assembly&#8221;**  
For example, let&#8217;s say I&#8217;ve got a few teams working on different modules for my new application, let&#8217;s call them &#8220;persistence&#8221;, &#8220;rest-api&#8221; and the user-interface, &#8220;ui&#8221;. Each of these modules depends on a set of common utility classes in &#8220;util&#8221;.

We can represent this through a set of triples like so:

rest-api depends-on persistence  
rest-api depends-on util  
ui depends-on rest-api  
persistence depends-on util (directly, and not only on the transitive dependency through persistence)

The unseen aspect here is the versioning. If we include versions in our triples, we see the picture is a bit more sophisticated:

rest-api-1.0 depends on persistence-3.1  
rest-api-1.0 depends-on util-1.1  
ui-1.0 depends-on rest-api-1.0  
persistence-3.1 depends-on util-1.0

Now we have a fully defined dependency graph that we can assemble into an application, say app-1.0. At any time, if we want a copy of the app in 1.0 state, we re-construct it from this deployed modules, no need to build any source code, and we&#8217;ve got the exact same app, every time.

**Get it in motion&#8230;**  
Now let&#8217;s look at this in a dynamic development environment, where we&#8217;re trying to maximize sustainable velocity:

Although there are dependencies between each module, we don&#8217;t want to hold up one team by forcing them to build the other teams modules unnecessarily. We also want each team to choose if they want to work with the very latest version of the other modules, or working against a fixed and stable version for a time instead. 

The &#8220;ui&#8221; team, for example, might be refactoring JavaScript code that&#8217;s relying on version 1.0.3 of &#8220;rest-api&#8221;, while &#8220;rest-api&#8221; in turn is already working on 1.0.4 &#8211; and it uses 1.1.0 of &#8220;persistence&#8221;&#8230; it can get tangled in a hurry without a way to manage it, and we don&#8217;t want to be artificially discouraged from writing modular code just because it&#8217;s hard to keep version numbers straight.

Enter Maven again. Instead of forcing everyone to just always work with the latest version of every other module (which can bring productivity to a screeching halt in some situations), we allow each time to decide what dependency they will include in their POM (Project Object Model) file. 

What if I want the very latest version of &#8220;persistence&#8221; while I work on &#8220;rest-api&#8221;, with changes checked in by other developers while I&#8217;m still working? This is where the SNAPSHOT version comes into play. Instead of declaring a dependency on 1.1.0, I declare a dependency on 1.1.1-SNAPSHOT. This represents the latest &#8220;edge&#8221; code for the referenced dependency.

Now we have a graph that looks like this:

app-1.0-SNAPSHOT depends on ui-1.1-SNAPSHOT  
rest-api-1.1-SNAPSHOT depends on persistence-3.1-SNAPSHOT  
rest-api-1.1-SNAPSHOT depends-on util-1.1  
ui-1.1-SNAPSHOT depends-on rest-api-1.1-SNAPSHOT  
persistence-3.1-SNAPSHOT depends-on util-1.1

As you can see, we have a mix of stable versioned modules (util in this case), and &#8220;on the fly&#8221; versions. Yet at the same time we&#8217;re assured that major changes that break backwards compatibility will **not** be seen, as we indicate such changes with a change in our major version number (e.g. 1.X to 2.0).

Then we can set up a CI job (say on TeamCity, Bamboo, or whatever your CI system of choice is) to automatically build and deploy our SNAPSHOT version of &#8220;persistence&#8221; to our local Maven repository (within our company firewall). The SNAPSHOT version actually turns into a date/timestamped version when it&#8217;s deployed to Nexus, and Maven is clever enough to fetch for us the most recent of these SNAPSHOTs every time we build. The &#8220;persistence&#8221; team checks in some code, CI builds it and deploys the resulting SNAPSHOT jar to our repository, and we get it automagically the next time we build, even though we&#8217;re working on rest-api, not persistence.

When we&#8217;re ready to &#8220;stabilize&#8221; our dependencies, we simply switch from the SNAPSHOT to a specific version. Maven has a pre-defined &#8220;release&#8221; process that guarantees, among other things, that every released version has no remaining SNAPSHOT dependencies, is tagged to version control, and verified via all it&#8217;s tests. More than a build tool indeed&#8230;

We could of course just put all the modules we&#8217;re going to depend on in an aggregator POM, and build **everything** every time we make a change, but this is hardly efficient, and limits our development velocity unnecessarily (and of course we might not all be in the same source tree, or even the same version-control repository). We want to be building smaller pieces, not bigger ones.

A critical part of this process is our company-local Maven repository &#8211; here I mean not just the developer-local repository on each developers own workstation, but a product like Nexus that holds a company-wide copy of all required jars for a build. By doing this, we can guarantee a consistent copy of all our required dependencies without having to depend on the availability of outside repositories, such as ibiblio. It&#8217;s not a bad idea to in fact \*only\* permit access to the local repository for building releases, which ensures this policy is not violated accidentally &#8211; while at the same time keeping the &#8220;external&#8221; maven repo&#8217;s available to developers for experimenting and prototyping. Once something gets used in production code, however, it gets stored in the &#8220;inside the firewall&#8221; Nexus repo (and backed up from there). This avoids the bad practice of checking jar files into source control (it&#8217;s called &#8220;source&#8221; control for a reason).

**Testing, Testing&#8230;**  
To add a new aspect to the problem, let&#8217;s say that it&#8217;s not only production code we depend on, but helper classes for tests as well. If it&#8217;s difficult to set up a fixture for a certain kind of test, that might be a code smell in and of itself, but that&#8217;s also another story. If we have some test helpers that reside in our dependent modules, we won&#8217;t be able to see those helpers in our tests in another module, as we&#8217;re only depending on that module&#8217;s production code, not test code.

We can easily tell Maven to **also** bundle up the test code from a certain module, however, and make it available to us in a jar file, like so:

<pre>&lt;code&gt;
 &lt;build&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-jar-plugin&lt;/artifactId&gt;
                &lt;executions&gt;
                    &lt;execution&gt;
                        &lt;goals&gt;
                            &lt;goal&gt;test-jar&lt;/goal&gt;
                        &lt;/goals&gt;
                    &lt;/execution&gt;
                &lt;/executions&gt;
            &lt;/plugin&gt;
            ...
     &lt;/plugins&gt;
&lt;/build&gt;
&lt;/code&gt;
</pre>

Now when we build, we&#8217;ll get a test jar as well as our regular jar, which we can depend on like so:

<pre>&lt;code&gt;
   &lt;dependency&gt;
            &lt;groupId&gt;com.point2.core&lt;/groupId&gt;
            &lt;artifactId&gt;somemodule&lt;/artifactId&gt;
            &lt;version&gt;1.0&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
            &lt;classifier&gt;tests&lt;/classifier&gt;
        &lt;/dependency&gt;
&lt;/code&gt;
</pre>

Now our test classes in the module declaring the above dependency can see the test helpers in the somemodule module &#8211; but we&#8217;re still not including test code in our production jar.

Again, I have to emphasize that this level of coupling might indicate a deeper issue, but if you do need to do this, it&#8217;s good to know how <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Automatic Dependency Management with Maven" class="wp-smiley" title="Automatic Dependency Management with Maven" /> 

Maven also includes facilities to analyze and clean up a complex dependency tree, remove unnecessary dependencies, and keep the whole project manageable.

In summary, Maven can handle extremely complex dependency management for us in a fully declarative and versioned manner, allowing us at any moment to see exactly what our project depends on, both in production and test code. In conjunction with a CI system (like TeamCity) and repository server (like Nexus), we can automate the deployment of intermediary and full-release versions to the point where we save significant time, and never build code that we&#8217;re not actually working on, allowing us to concentrate on the task at hand and leaving the heavy lifting to Maven.

This allows us to only ever build the code we&#8217;re actually changing &#8211; never code that&#8217;s already available in another library, reducing our developer cycle time significantly. It also means we&#8217;re spending more time &#8220;assembling&#8221; software from re-usable components than re-compiling (and probably re-testing) code that&#8217;s already verified and available in object form.

Maven: not just for breakfast anymore.