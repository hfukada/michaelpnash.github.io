---
title: 'OSGi Adventures, Part 2 &#8211; Dispatch Service and Dealer Service'
author: mnash
layout: post
permalink: /osgi-adventures-part-2-dispatch-service-and-dealer-service/
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
  - components
  - Java
  - Maven
  - modules
  - OSGi
  - ServiceMix
  - testing
  - unit
  - Vaadin
---
In [Part 1][1] of our OSGi adventures, we described how to build a nice Ajax-aware Vaadin UI app, and couple it to a generic back-end OSGi service we called the service dispatcher.

Now we&#8217;ll take the adventure to the next step, show how to deploy that webapp into our OSGi container and get it up and running, then go through the functionality of the Dispatch Service, and show how it routes requires through to the first of our domain-specific application services.

In our UI, we built a form that allowed the user to enter and save a &#8220;Dealer&#8221;, with some fields like name, phone number, etc., so the first service we&#8217;ll build for the service dispatcher to talk to will be our &#8220;dealer&#8221; service.

First, though, let&#8217;s see how to get our webapp into our OSGi container.

As we&#8217;re building our Vaadin app with Maven, we can easily add the small bits of additional configuration to turn our project into an OSGi-friendly WAR file. 

OSGi deploys &#8220;bundles&#8221;, but a bundle is just a jar file (or a war, which is after all just a special kind of jar) with a bit of extra meta-data. The META-INF/MANIFEST.MF file is where the magic happens. We add the following to our POM:

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
         &lt;plugin&gt;
                &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                &lt;artifactId&gt;maven-war-plugin&lt;/artifactId&gt;
                &lt;version&gt;2.0&lt;/version&gt;
                &lt;configuration&gt;
                  &lt;archive&gt;

                      org.springframework.osgi.web.context.support,
                       org.springframework.web.servlet,
                       org.springframework.web.servlet.handler,
                       org.springframework.web.servlet.mvc,
                       org.springframework.web.servlet.view,
                       dwmj.domain,
                       org.springframework.web.servlet.mvc.annotation,
                       org.springframework.web.context


                    &lt;manifestEntries&gt;
                      &lt;Bundle-ManifestVersion&gt;2&lt;/Bundle-ManifestVersion&gt;
                        &lt;Bundle-SymbolicName&gt;com.point2.Admin&lt;/Bundle-SymbolicName&gt;
                        &lt;Bundle-Name&gt;Admin&lt;/Bundle-Name&gt;
                        &lt;Bundle-Version&gt;1.0.0&lt;/Bundle-Version&gt;
                        &lt;Bundle-Activator&gt;com.point2.ServiceClient&lt;/Bundle-Activator&gt;
                        &lt;Import-Package&gt;org.osgi.framework,com.point2.services.dispatch,javax.servlet;version="2.4.0",
javax.servlet.http;version="2.4.0",org.osgi.service.http;version="1.2.0",
org.osgi.util.tracker;version="1.3.2"&lt;/Import-Package&gt;
                        &lt;Webapp-Context&gt;admin&lt;/Webapp-Context&gt;
                        &lt;Bundle-ClassPath&gt;WEB-INF/classes, WEB-INF/lib/service-dispatch-api-1.0.0.jar, WEB-INF/lib/vaadin-6.1.3.jar&lt;/Bundle-ClassPath&gt;
                    &lt;/manifestEntries&gt;
                  &lt;/archive&gt;
                &lt;/configuration&gt;
              &lt;/plugin&gt;
     &lt;/code&gt;
</pre>
</div>

This bit of magic allows Maven to build us a MANIFEST.MF like this:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
Manifest-Version: 1.0
Archiver-Version: Plexus Archiver
Created-By: Apache Maven
Built-By: mnash
Build-Jdk: 1.6.0_15
Extension-Name: admin
Implementation-Title: admin
Implementation-Version: 1.0-SNAPSHOT
Bundle-Activator: com.point2.ServiceClient
Bundle-ClassPath: WEB-INF/classes, WEB-INF/lib/service-dispatch-api-1.
 0.0.jar, WEB-INF/lib/vaadin-6.1.3.jar
Bundle-ManifestVersion: 2
Bundle-Name: Admin
Bundle-SymbolicName: com.point2.Admin
Bundle-Version: 1.0.0
Import-Package: org.osgi.framework,com.point2.services.dispatch,javax.
 servlet;version="2.4.0",javax.servlet.http;version="2.4.0",org.osgi.s
 ervice.http;version="1.2.0",org.osgi.util.tracker;version="1.3.2"
Webapp-Context: cadmin
&lt;/code&gt;
</pre>
</div>

Now we have our OSGi-friendly .war file, sitting in our target directory. We can then connect to the console of our OSGi container (in this case, ServiceMix), and say:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
install war:file:/Users/mnash/experiments/admin/target/admin-1.0.0-SNAPSHOT.war
&lt;/code&gt;
</pre>
</div>

Our container honors the &#8220;Webapp-Context&#8221; tag in our manifest, so we can then surf to http://localhost:8181/admin/ to see our application. 8181 is the default port for the Jetty HTTP service in ServiceMix &#8211; it can easily be changed to another number as required, of course.

**Dispatch Service**  
Now that we can see how to get the wepapp into ServiceMix, let&#8217;s look at the Dispatch Service in detail.

Our Dispatch Service is going to be a regular OSGi bundle, so we have a separate Maven project that produces a .jar file in this case, not a WAR file. 

Our MANIFEST.MF needs the following magic for this project:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.point2.services.dispatch.DispatchService
Bundle-Name: DispatchService
Bundle-Version: 1.0.0
Bundle-Classpath: .,lib/commons-beanutils-1.8.0.jar,lib/commons-collections-3.2.1.jar
Bundle-Activator: com.point2.services.dispatch.impl.DispatchServicePublisher
Import-Package: org.osgi.framework
Export-Package: com.point2.services.dispatch
&lt;/code&gt;
</pre>
</div>

You can see we&#8217;re again specifying a &#8220;Bundle-Activator&#8221; class, which, much like the ServiceClient class in our webapp, is called by the OSGi framework when the bundle containing this service is started.

One slight oddity: The dispatch service needs the two jars listed under &#8220;Bundle-Classpath:&#8221; to do it&#8217;s business &#8211; because we are building an OSGi bundle, we &#8220;embed&#8221; these jars in our bundle (which is, yes, another jar) by putting them in the src/main/resources/lib directory. We refer to them in that location in the POM, and Maven automatically includes them in the finished jar, where they&#8217;re available when our bundle needs them. The other alternative is to install the dependencies as their own bundles, but that&#8217;s a whole &#8216;nother post <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile OSGi Adventures, Part 2   Dispatch Service and Dealer Service" class="wp-smiley" title="OSGi Adventures, Part 2   Dispatch Service and Dealer Service" /> 

In the case of DispatchService, we&#8217;ve got an activator like this:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
public class DispatchServicePublisher implements BundleActivator {
    private ServiceRegistration registration;

    public void start(BundleContext context) throws Exception {
        registration = context.registerService(DispatchService.class.getName(),
                new DispatchServiceImpl(), null);
        DispatchServiceImpl.setBundleContext(context);
        System.out.println("Dispatch Service registered");
    }

    public void stop(BundleContext context) throws Exception {
        registration.unregister();
        System.out.println("Dispatch Service unregistered");
    }
}
&lt;/code&gt;
</pre>
</div>

Which simply takes a reference to the BundleContext on startup and passes it to the DispatchServiceImpl, which implements the DispatchService interface, like so:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
public interface DispatchService {
   List&lt;Map&lt;String, Object&gt;&gt; call(String serviceName, String serviceOperation, Map&lt;String, Object&gt; parameters,
                                  String versionPattern, String securityToken) throws Exception;
}
&lt;/code&gt;
</pre>
</div>

The big JuJu with OSGi is that **only** this interface is &#8220;exposed&#8221; from the bundle. No other service can see the innards of our service, unlike Jars on a classpath.

The implementation of the DispatchService is equally straightforward:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
public class DispatchServiceImpl implements DispatchService {

    private static BundleContext context;
    
    public List&lt;Map&lt;String, Object&gt;&gt; call(String serviceName, String serviceOperation, Map&lt;String, Object&gt; parameters, String versionPattern, String securityToken) throws Exception {

        ServiceReference reference = getServiceNamed(serviceName);
        if (reference == null)
            throw new RuntimeException("There is no service with service-name " + serviceName);
        Object service = context.getService(reference);
        Adapter adapter = new Adapter(service);
        List&lt;Map&lt;String, Object&gt;&gt; response = adapter.callList(serviceName, serviceOperation, parameters);
        context.ungetService(reference);
        return response;
    }

    private ServiceReference getServiceNamed(String serviceName) throws Exception {
        ServiceReference[] references = context.getAllServiceReferences(null, null);
        System.out.println("There are " + references.length + " services available");
        for (int i = 0; i &lt; references.length; i++) {
            ServiceReference reference = references[i];
            Object serviceNameValue = reference.getProperty("service-name");
            if (serviceNameValue != null) {
                System.out.println("I see service with name " + serviceNameValue);
                if (serviceNameValue.toString().equalsIgnoreCase(serviceName))
                    return reference;
            }
        }
        throw new RuntimeException("There is no service available with service-name " + serviceName);
    }

    public static void setBundleContext(BundleContext newContext) {
        context = newContext;
    }
}
&lt;/code&gt;
</pre>
</div>

The dispatch service implementation simply looks through the &#8220;published&#8221; services in the OSGi context, and looks at the &#8220;service-name&#8221; property of each service to find the one specified in the call. Assuming it finds an appropriate service, it then uses another class, Adapter, to do the type conversion of the generic Map of parameters to the specific types needed for the service being called, then uses Java reflection to actually make the call and return the response as a List of Maps, again converting the service-specific types to a generic Map in order to pass the response back to the user interface.

Why do we go through those gyrations, instead of just having access to the domain-specific beans in our UI? If we want a full decoupling, and the advantages that come with it, the type-independence of this approach gives us that. It also allows parallel development of the UI and the back-end services without an ever-increasing number of binary dependencies as well &#8211; for that matter, with the static data adapter in the Vaadin app allows us to develop on our UI entirely without the back-end services. That&#8217;s pretty decoupled. 

The Dispatch Service by itself, though, doesn&#8217;t give us any functionality. It acts much like a router on a network, simply moving the request from the client to the proper service on the back-end, so let&#8217;s build such a service &#8211; in this case, a service for handling Dealers.

**Dealer Service**  
The bulk of our application-specific code will be prepared as independent OSGi services, just like this one. In later postings, I&#8217;ll describe how to set up dependencies between services (and how to use Spring DM to make doing that kind of thing far simpler).

First, let&#8217;s look at our MANIFEST.MF for our new service (again, we can use Maven to produce this for us, but the result is the same):

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.point2.services.dealer.DealerService
Bundle-Name: DealerService
Bundle-Version: 1.0.0
Bundle-Activator: com.point2.services.dealer.impl.DealerServicePublisher
Import-Package: org.osgi.framework
Export-Package: com.point2.services.dealer
&lt;/code&gt;
</pre>
</div>

The two key elements above are the Bundle-Activator, a class called DealerServicePublisher, and the Export-Package.

OSGi best practices dictate that the package that is exported should only contain the interface for the class (or classes) you wish to make available from your service. In our case, that comprises a bean class, called &#8220;Dealer&#8221;, and the interface to our actual service, DealerService.

The Dealer bean is very simple, just your basic property-holding JavaBean:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
public class Dealer {
    private String name;
    private String phone;
    private String contactLast;
    private String contactFirst;
    private String address1;
    private String address2;

    public String getContactLast() {
        return contactLast;
    }

    public void setContactLast(String contactLast) {
        this.contactLast = contactLast;
    }

    public String getContactFirst() {
        return contactFirst;
    }
   .....
&lt;/code&gt;
</pre>
</div>

I&#8217;ve ommitted the rest of the getters and setters here for brevity (in case you&#8217;re wondering, yes, this is much easier to express in Scala, and yes, OSGi works just fine with Scala&#8230;)

The interface for our service is even simpler:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
public interface DealerService {
    public void save(Dealer dealer);
    public Dealer findById(int id);
}
&lt;/code&gt;
</pre>
</div>

Of course, a fully fleshed-out service might in fact have more methods, but again, you get the idea.

I won&#8217;t bore you with the actual implementation of the DealerServiceImpl class, but it&#8217;s important to note that it&#8217;s **not** in the same package as the Dealer bean and the DealerService implementation. They are the only two classes (well, one class, one interface) in that package, as the entire package is &#8220;exported&#8221; by OSGi, and therefore visible to other services and clients. 

The DealerServicePublisher is the last piece to examine, and it&#8217;s pretty straightforward as well:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
package com.point2.services.dealer.impl;

import com.point2.services.dealer.DealerService;
import org.osgi.framework.BundleActivator;
import org.osgi.framework.BundleContext;
import org.osgi.framework.ServiceRegistration;

import java.util.Dictionary;
import java.util.Hashtable;

public class DealerServicePublisher implements BundleActivator {
    private ServiceRegistration registration;

    public void start(BundleContext context) throws Exception {
        System.out.println("Registering dealer service");
        Dictionary dictionary = new Hashtable();
        dictionary.put("service-name", "dealer");
        registration = context.registerService(DealerService.class.getName(),
                new DealerServiceImpl(), dictionary);
    }

    public void stop(BundleContext context) throws Exception {
        System.out.println("Unregistering dealer service");
        registration.unregister();
    }
}
&lt;/code&gt;
</pre>
</div>

Essentially all we do in this activator is &#8220;register&#8221; our service, making it visible to the OSGi container and other services or clients that need it. We add an extra property via the &#8220;Dictionary&#8221; object, which allows us to specify arbitrary properties to be associated with our service. Because we want to look up our services from the dispatcher by name, rather than by class or interface name, we use the string &#8220;dealer&#8221; and associate it with the key &#8220;service-name&#8221;. If you examine the code for our DispatchService, you&#8217;ll see that it uses this property to find services.

Now we can build our new service with a simple &#8220;mvn package&#8221; command, and install the resulting jar into our OSGi runtime with &#8220;install file:/Users/mnash/experiments/dealer/target/dealer-1.0.0.jar&#8221; (again, you can do an install directly from the Maven repository, or from a URL, as opposed to a file).

That&#8217;s it &#8211; our &#8220;dealer&#8221; service is now available, and our &#8220;dispatch&#8221; service is fired up and ready to locate it. 

If we deploy our Vaadin application in our OSGi container (as described in the previous post), you&#8217;ll find that calls to the &#8220;call&#8221; method of the ServiceClient now return the &#8220;real&#8221; data from our service.

In the next few posts we&#8217;ll examine an even easier way to define new services, and explore the power of OSGi for updating and working with our decoupled services. Then we&#8217;ll look at how to hook services together, allowing services to call other services to do their jobs as required.

 [1]: http://php.jglobal.com/blog/?p=602