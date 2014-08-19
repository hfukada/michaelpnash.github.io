---
title: 'Maven&#8217;s Release Mechanism'
author: mnash
layout: post
permalink: /mavens-release-mechanism/
related_exlink_5_desc:
  - 
related_exlink_5:
  - 
related_exlink_4_desc:
  - 
related_exlink_4:
  - 
related_exlink_3_desc:
  - 
related_exlink_3:
  - 
related_exlink_2_desc:
  - 
related_exlink_2:
  - 
related_exlink_1_desc:
  - 
related_exlink_1:
  - 
categories:
  - Review
  - Software Design
tags:
  - deploy
  - Java
  - Maven
  - open source
  - release
  - stage
---
I&#8217;ve blogged a few times about how <a href="maven.apache.org" target="_new">Maven</a> and it&#8217;s associated tools and plugins is much more than a build tool, it&#8217;s a project information and management framework, so it&#8217;s no secret that I&#8217;m a fan.

One of the lesser-known things about Maven&#8217;s project management abilities is in it&#8217;s [release plugin][1] &#8211; the ability for Maven to co-ordinate and manage your release process in a reliable, simple, and fully-automated way. That&#8217;s what I&#8217;d like to explore here.

If we&#8217;re developing in an environment that supports a fully deterministic build process, including dependencies (binary and source), then we need to be able to version all our build artifacts, whether they are jar files, war files, or any other kind of file. During the development process, we need to be able to assemble applications quickly without compiling any more than we need to, and without being forced to release modules that are still moving targets. This is accomplished in Maven by use of the &#8220;SNAPSHOT&#8221; versions of modules. A module, let&#8217;s say &#8220;app&#8221;, that produces a jar file, is at any point at some specific version, let&#8217;s say &#8220;1.1&#8243;. Once we create the artifact for 1.1, our next creation of that jar must not re-use 1.1, it must be something else, as changes are incorporated.

If we&#8217;re not ready to release 1.2 (and we probably aren&#8217;t if we just released 1.1, we need an &#8220;intermediary&#8221; between 1.1 and 1.2. This is 1.2-SNAPSHOT. By seeing the &#8220;SNAPSHOT&#8221; we know we&#8217;re dealing with a version that may and probably will change. Internally, Maven translates the &#8220;-SNAPSHOT&#8221; to a date/timestamp and serial-number combination that allows you to track quite precisely each SNAPSHOT version as it changes, if you want, but generally you just want &#8220;the latest&#8221; (like HEAD from Subversion), and this is just called &#8220;SNAPSHOT&#8221;. 

When we want to release a new stable version, however, we want to reverse this process &#8211; we need to produce a new non-SNAPSHOT of our artifact, then immediately switch to the next SNAPSHOT version so that development can continue without interruption. In the case of our example, we&#8217;re going to produce app-1.2.jar, then immediately begin working on 1.3-SNAPSHOT.

During development, we may also want to specify our dependencies as SNAPSHOT versions as well, so if we have a dependency that is also in development, we can work on &#8220;the latest&#8221; version as well. Once we&#8217;re ready to release, though, this changes &#8211; we want only stable and reproducible code in our release, so we need to &#8220;resolve&#8221; all SNAPSHOT dependencies to a specific version, then we can switch our own module to a release version, probably tag the code at that point in SVN, and create the releaseable artifact. We probably also want to deploy that artifact to a staging area, ready to be deployed into our production environment.

Maven&#8217;s [release plugin][1] does all of this for us, and more, in a reliable and fail-safe way.

Run in two phases, the plugin&#8217;s goal &#8220;prepare&#8221; does all of the verification work for us. It:

1.  Verifies that there are no changes not yet committed to version control (so you&#8217;re sure you can reproduce this release from the checked-in code)
2.  Runs all tests, builds the project to ensure it passes it&#8217;s tests
3.  Verifies that there are no dependencies (direct or transitive) on SNAPSHOT intermediate versions (again, so the release is fully reproducable and stable) 
    *   *   Increments the version number in the project POM (or POMS, if you&#8217;re doing a multi-module release) to the new version (prompting for the next version number to use)
        *   Modifies the source code management information in the POM to point to the tagged version of the code
        *   Commits the changes made above to subversion (or your system of choice)
        *   Tags the code in the source control system (so you know exactly what code produced this release)
        *   Increment the version number again, now to the next SNAPSHOT version (again, prompting for the new value with sensible defaults)
        *   Commit the change to the new SNAPSHOT version</ol> 
        The goal &#8220;perform&#8221; actually performs the release, doing all the steps required to produce and publish a versioned artifact to our staging area (often a system such as Nexus), where it can be accessed as required to deploy to other environments.
        
        The perform process:
        
        1.  Checks out the code from source control from the proper tag
        2.  Produces the versioned artifact and deploys it to the staging area (usually Nexus or similar)
        3.  Produces the project website (with mvn site) and deploys that to it&#8217;s destination, recording information about the release, notes, and so forth
        
        There are other goals for recovering a failed release, doing &#8220;dry runs&#8221; of a deploy without actually changing anything, and even moving the deployed artifact into the target environment.
        
        So why might you choose Maven&#8217;s deployment process over a custom-built scripted process?
        
        There&#8217;s a few things you might consider when making such a choice:
        
        1.  Nothing to build: Maven&#8217;s release process is already written and finished, nothing to construct. This means less time to get an automated deployment process in operation, no matter how fast you can construct one, with Maven&#8217;s auto-discovery of plugins, it won&#8217;t be as fast as typing &#8220;mvn release:prepare&#8221;. You can apply Maven to a new project in seconds, as there&#8217;s nothing to configure or install, no scripts to write or edit.
        2.  Complete: Maven covers all the essential steps in a release automatically, so there&#8217;s no chance of leaving something out &#8211; like forgetting to tag SVN at the right moment or a SNAPSHOT dependency slipping into a production release
        3.  Standardized and Proven: A new user that knows Maven who is starting with your project has almost nothing to learn &#8211; the Maven release process is standardized and well-tested in thousands of high-volume sites. 
        4.  Integrated: The Maven release process works with all of the other project management tools that Maven brings to your project, such as reporting, staging, site generation, automated testing, and hundreds of others. Maven&#8217;s integration with tools like Nexus for staging and storing build artifacts allows you to manage component modules easily , permitting roll-out **and** roll-back of versions in a reliable and repeatable way.
        5.  Vendor-independent: The release plugin, like Maven itself, is vendor-agnostic, and works with any IDE, any CI server, and deployment scenario.
        6.  OSGi-Ready: A wealth of tools to handle OSGi bundle generation are supported by Maven and fully compatible with the release process, setting your project up to take advantage of the power of OSGi when you&#8217;re ready for it.
        7.  Dependency-Aware: Maven&#8217;s project management handles the complexity of multi-module/multi-component software &#8220;assembly&#8221;, a critical aspect of highly productive short-cycle development with on-demand release and deployment schedules, and the release plugin makes sure that the proper inter-module dependencies are observed and transient versions resolved before every deployment, automatically. Without such a tool, your teams will be tempted to build larger more monolithic applications, just because they&#8217;re easier to provision, release and deploy &#8211; always a poor reason to avoid componentization.
        8.  Multilingual: Maven and the release plugin can work with many different languages, not just Java, giving you a standardized deployment process across  
            a modern multi-language development environment easily.
        9.  Highly extensible and customizable: Because it&#8217;s open source, you have full control over the operation of Maven and it&#8217;s deploy process in a way that&#8217;s not possible with non-open products. Even without using the available source, configuration can bind custom operations to every lifecycle phase of a release&#8217;s process easily.
        
        In short, rolling your own process for deployment is a much more expensive and risky proposition than using a reliable and well-established tool such as Maven to do it for you.

 [1]: http://maven.apache.org/plugins/maven-release-plugin/