---
title: 'ServiceMix 4: Getting on the Bus'
author: mnash
layout: post
permalink: /servicemix-4-getting-on-the-bus/
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
  - Review
  - Software Design
tags:
  - Apache
  - components
  - configuration
  - design
  - ESB
  - integration
  - Java
  - JBI
  - open source
  - OSGi
  - ServiceMix
  - SOA
---
The Apache Group have recently released version 4 of the [ServiceMix ESB.][1] (Enterprise Service Bus), and I had a chance to work with it a bit over the weekend.

As we develop more and more services, the plumbing is starting to get complicated. We&#8217;re starting to ask questions like what versions of what services do we have? What dependencies do we have between services? How can/should we deploy services? Should we use REST or JMS for this service? How can we easily manage and monitor all these services in a fully clustered, scalable and high-availability environment?

In short, how can we develop powerful scalable services **fast** and not worry about the plumbing?

We&#8217;re not the only people to have asked these questions &#8211; and one powerful answer is to use an ESB.

ESB&#8217;s have come a long way, and the [JBI standard][2] and [OSGi][2] finally get together in this version of ServiceMix, and some pretty powerful magic happens as a result.

Just about every organization that writes sophisticated applications, particularly Java applications, have run into some of the problems that an ESB provides solutions for &#8211; the same is true of OSGi.

As Anthony Juckel put it on [his blog][3], &#8220;*Any sufficiently complicated Java program contains an ad hoc, informally-specified, bug-ridden, slow implementation of half of OSGi.*&#8220;. This is quite true, in my experience, and can even be extended to include ESB&#8217;s, in that if you&#8217;ve got a number of JVM services interacting on a network to solve a problem, you&#8217;ve got some kind of an ESB going on, whether you call it that or not.

A common practice recently is to write software that provides &#8220;services&#8221;, then to combine these services into a complete system &#8211; in other words, we write services, but we **compose** systems (from these services). The awkward part comes (well, **one** awkward part) when we try to write the service in such a way that it can be used in many different ways &#8211; in other words, to maximize the potential for re-use &#8211; while at the same time trying to do the simplest thing that can possibly work.

No matter what service mechanism we choose, we lock ourselves in to some degree. If we write our service to use JMS (Java Messaging System), so we can support nice events and queues and other asynchronous goodness, we can&#8217;t easily then use our service from, let&#8217;s say, a client that looks for a REST service. If we choose SOAP, we can&#8217;t easily talk to our service from a client (which could be another service) that wants to post an event, instead of call a SOAP interface.

**Normalized Messages**  
The Java JBI (Java Business Integration) standard answers this problem: it provides a single message-oriented interface for services, called the Normalized Message. This Normalized Message contains some header info, some properties, and XML payload, and optionally, binary attachments. It is not specific to any one protocol &#8211; in other words, it&#8217;s not SOAP, it&#8217;s not REST, it&#8217;s not JMS, it&#8217;s not SMTP, it&#8217;s not any of those.

JBI is a JSR for defining Java Business Integration, a way to cut through the complexity of different types of communications mechanisms for component message-passing (e.g. things such as REST, JMS, SOAP, RPC, email, FTP, HTTP, file system, and so on).

ServiceMix is one of several choices &#8211; once we have services written to the JBI standard, we can deploy them in any JBI-compliant ESB. Glassfish&#8217;s OpenESB is another option, for example.

Instead of worrying about the plumbing of the specific protocol we want to use, we can concentrate on writing our business logic, then rely on the ESB to &#8220;wire up&#8221; the messages between our service-providing components &#8211; whether they&#8217;re local (e.g. running in the same ESB, in which case it&#8217;s a simple in-memory message), or distributed, on another box in our cluster, or halfway around the world. The ESB provides adapters for each of the different protocols &#8211; so we can take our one service and talk to it via REST, JMS, SOAP, Email, carrier pigeon (ok, maybe not the last one &#8211; but you **could** write an adapter!).

This means I can write my service without even knowing what kind of protocol I&#8217;m going to be talking to it with &#8211; maybe it receives some messages via JMS, some via REST calls, a couple of SOAP services, and one in a while via an email. All that is the problem of the ESB &#8211; I just write one simple method in one simple interface to swallow the appropriate NormalizedMessage, do my processing whatever it is, and spit back out another NormalizedMessage.

This can **significantly** speed up the development of new services, by taking decisions about the plumbing away from the process of writing the correct business logic. We don&#8217;t even need to decide up-front if our service will be used by other services or not &#8211; we can wire it up as required.

The other important thing about a Normalized Message is that it refers to services by an identifier, but not by a specific location &#8211; in other words, a message from a client might say &#8220;I need this service to process this message&#8221;, but it&#8217;s up to the bus to figure out how to get the message to the service &#8211; this provides the opportunity to decouple services from each other. Let&#8217;s say you need to write a service that takes some kind of business message and sends an email. You don&#8217;t have to worry about passing your service information to let it find the email service at all &#8211; you just send the message to a service name (maybe &#8220;email&#8221;), and the ESB figures out the rest.

This means you can swap the email service out for another service that provides the same mechanism without worrying about the details.

**JBI and OSGi Together**  
ServiceMix is one example of such an ESB, which marries the modularization advantages of OSGi with the above-described benefits of an ESB. This means each of our components can run in it&#8217;s own classpath space, with no interference with other components &#8211; even other components that might use different versions of the same jars. How many times have you discovered you&#8217;ve got 3 different versions of log4j on your classpath? This can lead to all sorts of weird and wonderful problems that only occur in certain circumstances, and are all-but-impossible to fix. By providing **true** modularization, OSGi solves this problem properly. Other solutions that I&#8217;ve seen applied in the past lead directly to the quote about every complex system having a half-baked OSGi implementation inside them <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile ServiceMix 4: Getting on the Bus" class="wp-smiley" title="ServiceMix 4: Getting on the Bus" /> 

ServiceMix also provides a whack of existing components in two different JBI flavors: Service Engines and Binding Components. Services Engines are the ones that do the actual business logic, and Binding Components are the adapters, the pieces that route messages to and from various protocols. Many common tasks can be achieved by configuring the existing pieces, without writing a line of code.

When it is necessary to write some code, ServiceMix includes adapters to make that even easier as well &#8211; for instance, it provides a Service Engine to allow any POJO (plain old java object) to be used as a service, without that object having to actually implements the interface for handling NormalizedMessages directly. It doesn&#8217;t get any easier than that to write a service &#8211; just write the bean, plug in a bit of configuration, and you&#8217;re done &#8211; instance REST (JMS, email, SOAP, etc etc) service!

Spring integration is built into ServiceMix, so SE&#8217;s can have their dependencies injected automagically on deployment. 

SE&#8217;s can be hot-deployed and hot-removed. Multiple versions of a single SE can be running without conflict, so &#8220;hot&#8221; upgrades can be done easily. You can have one version of a service that requires version 1.1 of another service running at the same time as some other service that requires 1.2 of the same service. This is flexibility in deployment, as it means that there&#8217;s no need to &#8220;drag along&#8221; other services when upgrading if you don&#8217;t want/need to.

Services can easily be managed and monitored via the administrative capabilities of the bus.

**Binding Components**  
Binding components are how we talk outside the backbone &#8211; they take messages from the backbone and transmit or receive via an external protocol to non-ESB services &#8211; e.g. via REST, JMS, HTTP, file system, etc etc. There are dozens of existing binding components to support just about every protocol we&#8217;d care about.

Of course, all this power comes with a price: you have to learn to manage and deploy your ESB of choice, and even the simplest ESB is still a fairly complex beast. ServiceMix is no exception. The good news, however, is that it&#8217;s possible to pretty much ignore much of the available complexity in order to get started small, then learn more as you need it to start to leverage the power available. 

A caveat, however: It&#8217;s important to use an ESB the way it&#8217;s intended, and not try to shoehorn things that don&#8217;t fit into it&#8217;s structure. If you find yourself struggling to write services, or having to write a lot of Binding Components, chances are you&#8217;re making inappropriate design decisions, or that you haven&#8217;t separated the concerns of a Service Engine from a Binding Component fully. This is not uncommon, as in many environments these two concerns are handled by a single component. If you&#8217;re using to writing REST services, for instance, with things such as JRA or Jersey, you&#8217;ll find it very odd to separate the processing from the &#8220;presentation&#8221; (even when that presentation is simply into XML or JSON to the REST client).

Once this technique becomes second nature, however, the true power of an ESB becomes clearer.

**A whole fleet of buses&#8230;**  
Multiple ESB instances can be deployed and clustered, providing highly scalable and fault-tolerant system. The communication between ESB instances is handled entirely by the ESB itself &#8211; nothing about our components needs to be aware that they&#8217;re working in a clustered environment.

From my latest look at ServiceMix and it&#8217;s new release, I suspect I&#8217;ll be taking a deeper dive in the near future.

(Thanks to [Craig Walls][4] for pointing out that excellent quotation &#8211; and for all his help in [understanding OSGi!][5])

 [1]: http://servicemix.apache.org/SMX4/index.html
 [2]: http://www.osgi.org/Main/HomePage
 [3]: http://sputteringdigitized.blogspot.com/2009/08/paraphrase-of-greenspuns-tenth-rule.html
 [4]: http://www.jroller.com/habuma/
 [5]: http://www.pragprog.com/titles/cwosg/modular-java