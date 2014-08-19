---
title: Continuous Releasability with Maven and TeamCity
author: mnash
layout: post
permalink: /continuous-releasability-with-maven-and-teamcity/
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
On a recent project I&#8217;ve had the opportunity to help set up a new method of producing our software releases. We had a number of goals in setting up this process, and I think we&#8217;ve done pretty well in acheiving them. Some of these were:

*   Each product should produce a single artifact as part of it&#8217;s continuous integration build cycle.
*   Each artifact should be a release candidate.
*   The product should be releaseable at all times, just with more and more functionality being added over time.
*   Each artifact should be versioned sufficiently that we can exactly reproduce the source code it was built from from our source control system (currently SVN).
*   Each release candidate artifact should be self-contained and ready to be installed on everything from local workstations to the production environment without modification or external configuration
*   Developers should not be inconvenienced by the build/release process at all &#8211; they just check in their work and keep going
*   Each release candidate should be automatically deployed to a test environment where automated acceptance tests can be run against it.
*   Each release candidate should be tested via a suite of automated acceptance tests, and it should be clear which candidates pass that suite.
*   Each release candidate should be deployed automatically to an exploratory test environment so the customer proxy can work with it interactively to further approve it for deployment to the customer, or not
*   It should be the customer proxy&#8217;s decision whether or not to send a particular release candidate to the customer or not. He should not require developer input to that decision.
*   The build and install process we use should be the exact same for all environments.
*   Once a release candidate is produced, it should be the exact same artifact all the way to production, no changes, no re-building.
*   </ul> 
    In our environment we produce two applications at the moment, which are both part of the same suite of applications and communicate with each other when deployed. We have an automated integration test that verifies they communicate correctly.
    
    One application is packaged as an EAR (Enterprise Application aRchive) file, and is deployed to a cluster of Weblogic servers. The other is packaged as a group of OSGi bundles, one of which is also a web application (WAR) file. We have automated the build/test/release process in the same way for both products, although their install process is of course quite different.
    
    Let me walk through how our process works, starting from the point where a developer checks in some code that implements a new feature (or some other story given to us by the customer proxy).
    
    1.  The developer builds and checks his change locally (using the same build and install process as the rest of the sequence, but I&#8217;ll skip those steps for clarity for now, as they&#8217;re the same as the steps below).
    2.  Our TeamCity server notes a change in the Subversion repository for the appropriate product (let&#8217;s say it&#8217;s the Weblogic-based one for now), and triggers the CI job
    3.  The CI job checks out the latest revision from Subversion and triggers a Maven &#8220;clean install&#8221; target. Our projects both consist of multiple modules with an aggregator POM, that is, a POM file that describes a set of subordinate modules, each of which also has it&#8217;s own POM file. This is helpful for both development and building, as when developing, you can choose to open the aggregator POM with your IDE (we mostly use JetBrains IntelliJ IDEA) if you&#8217;re refactoring accross modules, or you can open just one of the components if that&#8217;s all you&#8217;re working on.
    4.  The aggregator POM does a compile and test cycle on each subordinate module, running both it&#8217;s unit and functional tests (we use an annotation to separate the two -but that&#8217;s another blog post)
    5.  In the aggregator POM we have two important plugins configured. The first is the &#8220;Build Number&#8221; plugin, which reads the meta-data from the SVN checkout and determines the global revision number that it just checked out. This number is then used in a couple of places: first, it&#8217;s built into the MANIFEST.MF file of the resulting artifact, so that we can tell exactly where this source code came from. Secondly, it&#8217;s written into a properties file (via the Maven properties plugin) for use in the installation process later. The second plugin is the &#8220;assembly&#8221; plugin. This tells Maven to collect all of the produced artifacts from the build of all of the modules into a single ZIP file, which we&#8217;ll describe in more detail below.
    6.  When the &#8220;assembly&#8221; plugin triggers (at the end of the &#8220;install&#8221; lifecycle phase, which we tell it to do via configuration in the POM), Maven automatically builds us a zip file. Through an additional option, we tell this zip file to include a set of installation scripts. In the case of our Weblogic app, these are Jython scripts that configure the target Weblogic server properly, then deploy the application to the entire cluster at once.
    7.  The zip file that assembly produces has two version numbers in it&#8217;s name (and inside it). The first is the version number from the aggregator POM, which is the &#8220;public&#8221; version of the application, e.g. 3.1.18 or such. As developers, we don&#8217;t care about this version at all, and don&#8217;t set it &#8211; our customer proxy determines it. The second number is the SVN revision number, which we care about more, as it tells us exactly what point in the source code our artifact was built from.
    8.  The TeamCity server now completes the initial CI job, and retains the versioned artifact. It might have a name like &#8220;productx-3.1.18-r1234.zip.
    9.  Like most CI servers, TeamCity can then trigger the next dependant job, which in this case copies the artifact from the initial job and uses Ant to SCP it to our automated test cluster, unzip it, and trigger the embedded install script. Bundling the installer with the product means that when the installation needs to change, we just change the script and it goes out automatically, versioned the same was as the code it&#8217;s installing.
    10. Now the &#8220;deploy to test cluster&#8221; job is complete, and an series of automated acceptance tests are triggered against the test cluster by TeamCity. If these pass, the test job also gets a copy of the original artifact, and retains it. This is the point where the customer proxy can do exploratory testing against the test cluster if desired, and make up his mind if the release candidate is of sufficient quality and utility to be shipped to the customer. If so, he &#8220;pins&#8221; the build in TeamCity to leave a note, and ships the zip file off to the end-user for their installation.
    11. At this point the customer proxy might want to bump the &#8220;public&#8221; version number, and he can simply change the version in the aggregator POM file to do so. The developers don&#8217;t care &#8211; they are concerned with versions only of the sub-modules, as some of them depend on other sub-modules. 
    
    For our OSGi-based product we use the exact same process, with the exception that the installer is Java/JMX based instead of a set of Jython scripts. In both cases, the user of the artifact to be installed just unzips the file and says &#8220;install.sh&#8221; (or install.bat).
    
    We don&#8217;t use the Maven release plugin for this process at all, as it &#8220;tags&#8221; at the end of the build cycle, not the beginning. We don&#8217;t even necessarily need to use SNAPSHOT versions, as the version of the actual internal modules are never visible to the customer in any case, and we rachet to the target release number at the beginning of the release development cycle, not the end &#8211; in other words, if we&#8217;re heading towards releasing 3.2 of the product, the customer proxy changes (or asks us to change) the version of the aggregator POM to 3.2 immediately. Then we produce 3.2-r1234, 3.2-r1235, 3.2-r1236 and so forth until the customer proxy says &#8220;ok, it&#8217;s done&#8221;, at which point he (not we) sends it off to the customer, and bumps us to 3.3.
    
    This is quite a different sequence than many teams use, although I have used it before (although not with TeamCity).
    
    So far it&#8217;s working for us, we&#8217;ll report if we find things to optimize about it.
    
    Comments and/or questions are most welcome!
    
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