---
title: 'OSGi Adventures, Part 1 &#8211; A Vaadin front-end to OSGi Services'
author: mnash
layout: post
permalink: /osgi-adventures-part-1-a-vaadin-front-end-to-osgi-services/
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
  - Review
  - Scala
  - Software Design
tags:
  - components
  - design
  - hot deploy
  - Java
  - Maven
  - OSGi
  - Vaadin
---
In my experience, the future of modularity on the JVM is OSGi.

Many developers don&#8217;t seem to recognize the need for it, but other bloggers have covered this in great detail (see my Resources page for some links), so I&#8217;m not going to try to &#8220;sell&#8221; OSGi here at all &#8211; I assume you&#8217;re already sold, and looking at how to put OSGi to good use in your development and deployment process.

Extending my recent experiments with the Vaadin framework, I decided I wanted to have a Vaadin front-end talking to a set of OSGi services on the back end. Initially, these will be running within the same OSGi container, which in this case is FUSE 4, the commercially supported variant of Apache ServiceMix.

One of my goals was to acheive a loose coupling between the Vaadin webapp and the backing services, so that new services can readily be added, started, stopped, and updated, all without any impact on the running Vaadin app. I also wanted to maintain the convenience of being able to run and tinker with the UI portion of my app by just doing a &#8220;mvn jetty:run&#8221;, so the app needed to be able to start even if it wasn&#8217;t inside the OSGi container.

Fortunately, doing all this is pretty easy, and in the next series of articles I&#8217;ll describe how I went about it, and where the good parts and bad parts of such an approach became obvious.

In this part, we&#8217;ll start by describing the Vaadin app, and how it calls the back-end services. In later parts, I&#8217;ll describe the evolution of the back-end services themselves, as I experimented with more sophisticated techniques.

**Vaadin Dependency**  
I&#8217;m building all my apps with Apache Maven, so the first step was to create a POM file suitable for Vaadin. Fortunately, Vaadin is a single jar file, and trivial to add to the classpath. My POM needed this dependency:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
       &lt;dependency&gt;
            &lt;groupId&gt;vaadin&lt;/groupId&gt;
            &lt;artifactId&gt;vaadin&lt;/artifactId&gt;
            &lt;version&gt;6.1.3&lt;/version&gt;
            &lt;scope&gt;system&lt;/scope&gt;
            &lt;systemPath&gt;${basedir}/src/main/webapp/WEB-INF/lib/vaadin-6.1.3.jar&lt;/systemPath&gt;
        &lt;/dependency&gt;
     &lt;/code&gt;
</pre>
</div>

Here I&#8217;m using the trick of specifying a systemPath for my jar, instead of retrieving it on demand from a local Nexus repository or from the internet, but that&#8217;s just one way of doing it &#8211; the main thing is to get this one Vaadin jar on your path.

**web.xml**  
Next I proceeded to tweak my web.xml to have my top-level Vaadin application object available on a URL. The main Vaadin object is an extension of a Servlet, so this is also very easy &#8211; here&#8217;s my web.xml in it&#8217;s entirety:

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns="http://java.sun.com/xml/ns/javaee" xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5"&gt;
  &lt;display-name&gt;Admin&lt;/display-name&gt;
  &lt;servlet&gt;
    &lt;servlet-name&gt;Admin&lt;/servlet-name&gt;
    &lt;servlet-class&gt;com.vaadin.terminal.gwt.server.ApplicationServlet&lt;/servlet-class&gt;
    &lt;init-param&gt;
      &lt;param-name&gt;application&lt;/param-name&gt;
      &lt;param-value&gt;Admin&lt;/param-value&gt;
    &lt;/init-param&gt;
  &lt;/servlet&gt;
  &lt;servlet-mapping&gt;
    &lt;servlet-name&gt;Admin&lt;/servlet-name&gt;
    &lt;url-pattern&gt;/*&lt;/url-pattern&gt;
  &lt;/servlet-mapping&gt;
&lt;/web-app&gt;
&lt;/code&gt;
</pre>
</div>

In this situation my &#8220;Admin&#8221; class is in the default package, which is not generally a good practice, but you get the idea.

**Menu and MenuDispatcher**  
I then used the &#8220;Tree&#8221; class in Vaadin to build myself a nice tree-style menu, and added that to the layout on my main page. My main page has some chrome regions for a top banner and other assorted visual aids, then a left-side area where the menu lives, and a &#8220;main&#8221; area, where all the real action in the application will happen.

A class I called MenuDispatcher &#8220;listens&#8221; for events on the menu (e.g. the user clicking something), and does the appropriate action when a certain menu item is clicked.

Here&#8217;s the interesting bits from the MenuDispatcher &#8211; as you can see, it&#8217;s constructed with a reference to the &#8220;mainArea&#8221; layout when it&#8217;s first initialized.

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
public class MenuDispatcher implements ItemClickEvent.ItemClickListener {

    private VerticalLayout mainArea;

    public MenuDispatcher(VerticalLayout mainArea) {
        this.mainArea = mainArea;
    }

    public void itemClick(ItemClickEvent event) {
        if (event.getButton() == ItemClickEvent.BUTTON_LEFT) {
            String selected = event.getItemId().toString();

            System.out.println("Selected " + selected + " from menu");
            if (selected.equals("create dealer")) {
                createDealer();
            } else if (selected.equals("edit dealers")) {
                editDealer();
            } 
...
            }
            System.err.println("Selected " + event.getItemId());
        }
    }

    private void createDealer() {
        mainArea.removeAllComponents();
        Component form = new CreateDealerForm();
        mainArea.addComponent(form);
        mainArea.setComponentAlignment(form, Alignment.MIDDLE_CENTER);
        mainArea.requestRepaint();
    }

    private void editDealer() {
...
    }

...
}
&lt;/code&gt;
</pre>
</div>

Again, this code can be made more sophisticated &#8211; I&#8217;m thinking a little Spring magic could make adding new forms and such very convenient, but this gets us started.

**Submitting the Form**  
The &#8220;CreateDealerForm&#8221; object referred to in the Dispatcher then builds a Vaadin &#8220;Form&#8221; class, much like the example form built in the &#8220;Book of Vaadin&#8221;. The only interesting part of my form was that I chose not to back it with a Bean class, which is an option with Vaadin forms. If you back with a bean, then you essentially bind the form to the bean, and the form fields are generated for you from the bean. 

If I wanted to then send the corresponding bean to the back-end service, then binding the bean to the form would be a good way to go. Instead, however, I don&#8217;t want my back-end services to be sharing beans with my UI application at all. I&#8217;ll explain why and how later on in more detail.

The interesting part of my form, then, is how I handle the submission of the form:

Assuming I have a button on my form, defined like so:

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
 Button okbutton = new Button("Submit", dealerForm, "commit");
&lt;/code&gt;
</pre>
</div>

I can add a listener to this button (again, using Vaadin&#8217;s magic ability to route the Ajax events to my Java code) like thus:

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
 okbutton.addListener(new Button.ClickListener() {
            public void buttonClick(Button.ClickEvent event) {

                Map&lt;String, Object&gt; parameters = new HashMap&lt;String, Object&gt;();
                for (Object id: dealerForm.getItemPropertyIds()) {
                    Field field = dealerForm.getField(id);
                    parameters.put(id.toString(), field.getValue());
                }

                System.out.println("*** Calling dealer service via dispatcher");
                ServiceClient.call("dealer", "save", parameters, null, null);
                getWindow().showNotification("Dealer Saved");
            }
        });
&lt;/code&gt;
</pre>
</div>

I&#8217;m using an anonymous inner class to listen to the event, and the &#8220;buttonClick&#8221; method gets called when the user says &#8220;Submit&#8221;. 

The next steps are where the form meets the back-end service: First, I iterate over the form and build a map containing all the field values. The map is keyed with a string, for the name of the field or property, and the value in the map is the value the user entered. Note that these values are already typed &#8211; e.g. a checkbox can have a boolean, a TextField can have a string, a calendar field can have a java.util.Date. We retain these types, and wrap everything up in a map.

Now (after a quick println so I can see what&#8217;s going on), I call a static method on class called ServiceClient, sending along the name of the service I want to call, the operation on that service, and the parameter map I just built from my form.

The last line just shows a nice &#8220;fade away&#8221; non-modal notification to the user that the dealer he entered has been saved (assuming the call to ServiceClient didn&#8217;t throw an exception, which we&#8217;re assuming for the moment for simplicity).

So, now we have our &#8220;call&#8221; method to consider, where the map of values we built in our Vaadin front-end gets handed off to the appropriate back-end service.

**Calling the Service**

The only job of the ServiceClient object is to route a call from somewhere in our Vaadin app (in this case, the submission of a form) to the proper back-end service, and potentially return a response.

We identify our back-end services by a simple string, the &#8220;service name&#8221; (our first argument). The second argument to call tells us the &#8220;operation&#8221; we want from this service, as a single service can normally perform several different operations. For instance, our dealer service might have the ability to save a dealer, get a list of dealers, find a specific dealer, and so forth.

In Java parlance, a service operation might correspond to a method on the service interface, but we&#8217;re not coupling that tightly at this point &#8211; our service, after all, might not be written in Java for all we know at this point, and I prefer to keep it that way.

This is the &#8220;loose joint&#8221; in the mechanism between the UI and the back-end. To keep the joint loose, we don&#8217;t send a predefined Bean class to the back-end service to define the parameters to the service operation, we send a map, where that map contains a set of key/value pairs. The keys are always Strings, but the values can be any type &#8211; possibly even another map, for instance, which would allow us to express quite complex structures if required, in a type-independent fashion.

Let&#8217;s have a look at ServiceClient:

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
public class ServiceClient implements BundleActivator {

    private static DispatchService dispatchService = null;

    public void start(BundleContext context) throws Exception {
            ServiceReference reference = context.getServiceReference(DispatchService.class.getName());
            if (reference == null)
                throw new RuntimeException("Cannot find the dispatch service");
            dispatchService = (DispatchService) context.getService(reference);
            if (dispatchService == null)
                throw new RuntimeException("Didn&#039;t find dispatch service");
    }

    public void stop(BundleContext context) throws Exception {
        System.out.println("Stopping bundle");
    }

    public static List&lt;Map&lt;String, Object&gt;&gt; call(String serviceName, String operation, Map&lt;String, Object&gt; params, String versionPattern, String securityToken) throws Exception {
            if (dispatchService == null) {
                System.out.println("No OSGi dispatch service available - using dummy static data");
                return StaticDataService.call(serviceName, operation, params, versionPattern, securityToken);
            }
            return dispatchService.call(serviceName, operation, params, versionPattern, securityToken);
    }
}
&lt;/code&gt;
</pre>
</div>

Let&#8217;s go through that class piece by piece. First, you&#8217;ll notice that the class implements the BundleActivator interface &#8211; this tells the OSGi container that it is possible to call this class when the OSGi bundle containing it is started and stopped. During the start process, you can have the class receive a reference to the BundleContext. This is somewhat analagous to the Spring ApplicationContext, in that it gives our class access to the other services also deployed in OSGi. The Spring DM framework lets you do this kind of thing more declaratively, but it&#8217;s good to know how the low-level works before engaging the autopilot, I always find.

In order to allow BundleActivator to be found, we need another couple of things on our classpath, so we add this to our POM:

<div class="capsule" style="text-align: left">
  <pre>
     &lt;code&gt;
  &lt;dependency&gt;
            &lt;groupId&gt;org.osgi&lt;/groupId&gt;
            &lt;artifactId&gt;osgi_R4_core&lt;/artifactId&gt;
            &lt;version&gt;1.0&lt;/version&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;org.osgi&lt;/groupId&gt;
            &lt;artifactId&gt;osgi_R4_compendium&lt;/artifactId&gt;
            &lt;version&gt;1.0&lt;/version&gt;
        &lt;/dependency&gt;
&lt;/code&gt;
</pre>
</div>

This defines the BundleActivator interface and other OSGi requirements which we use.

As you can see, we use our reference to the OSGi context to get a ServiceReference to an interface called &#8220;DispatchService&#8221;. We&#8217;ll examine dispatch service in detail in my next posting, but for now you can see we hold on to our reference as an instance variable.

When the call to the &#8220;call&#8221; method happens, our DispatchService reference is already available if we&#8217;re running inside an OSGi container, all wired up and ready to go. To give us flexibility, though, we also allow for the case where dispatch service is null, meaning we&#8217;re **not** running inside and OSGi container.

Instead of crashing and burning, however, we simply redirect our call to a &#8220;StaticDataService&#8221; class, which does just what you might expect. For every call it understands, it returns a static &#8220;canned&#8221; response. This allows us to build and test our UI without actually having written any of the back-end services, and to continue to run our Vaadin app with a simple &#8220;mvn jetty:run&#8221;, when all we&#8217;re working on is look and feel, or logic that only affects the UI.

This means my &#8220;cycle time&#8221; to test a change in the UI code is a matter of seconds &#8211; when I do a &#8220;mvn jetty:run&#8221; my code is compiled and up and running in my browser in about 5 seconds, and that&#8217;s on my 5 year-old macbook laptop, so there&#8217;s no penalty for not having a dynamic language in the mix here, from my point of view.

If DispatchService is not null, however, then we&#8217;re running &#8220;for real&#8221; inside an OSGi container, so we use our stored reference to the dispatch service to &#8220;forward on&#8221; our call. The dispatch service works it&#8217;s magic, which we&#8217;ll examine in a later post, and returns a List of Map objects with our response. This list might only contain one Map, of course, if the service was a simple one.

The response is then returned to the caller elsewhere in the Vaadin application, to do whatever is necessary from a UI point of view &#8211; perhaps populate a form or table with the response data.

As we&#8217;ll see in detail in my next post, the dispatch service in this case acts as a &#8220;barrier&#8221; between the UI-oriented code in our Vaadin app and our domain-specific application logic contained in our services. It is responsible for mapping our generic map of parameters into whatever domain beans are used by our back-end services, and for figuring out which of those services should be called, and which operation on that service is required. Those services then return whatever domain-specific objects they return, and the dispatcher grinds them into non-type-bound maps, or lists of maps, if there is a whole series of returns. 

This means our Vaadin app only ever has to talk to one thing: the dispatcher. We only change our Vaadin code for one reason: to change the UI, never in response to a change of service code, even if the beans and classes of that service change significantly.

Next time we&#8217;ll look at the dispatch service and the first of our application-specific domain-aware services, and see how they come together.