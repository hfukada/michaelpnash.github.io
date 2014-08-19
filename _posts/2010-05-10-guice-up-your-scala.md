---
title: Guice up your Scala
author: mnash
excerpt: "How to use Google's Guice and Scala together"
layout: post
permalink: /guice-up-your-scala/
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
tags:
  - configuration
  - Guice
  - Java
  - junit
  - modules
  - OSGi
  - Scala
  - spring
---
In a project I was tinkering with lately I found the complexity getting to the point where I could use component dependency injection. There are in fact a [number of techniques][1] to do this in &#8220;plain&#8221; Scala, but they generally seem more painful to me than just dropping in a lightweight DI framework, so I went with [Guice.][2]

As it happens, Guice works with Scala very nicely, and is very unobtrusive. There&#8217;s a few minor things I haven&#8217;t quite figured out yet, but I&#8217;d like to share what I&#8217;ve discovered so far.

After adding this section to my project POM:

<pre class="brush:xml">&lt;dependency&gt;
            &lt;groupId&gt;com.google.inject&lt;/groupId&gt;
            &lt;artifactId&gt;guice&lt;/artifactId&gt;
            &lt;version&gt;2.0&lt;/version&gt;
        &lt;/dependency&gt;
</pre>

I had all I needed of Guice embedded in my app. Now I can scratch up a series of tests that exercise all of the different ways use Guice from Scala. Let&#8217;s start with the simplest, and work our way up:

<pre class="brush:scala">@Test
  def basicDependencyInjection {
    class ScalaModule extends AbstractModule {
      @Override
      protected def configure() {
        bind(classOf[AService]).to(classOf[SomeService])
      }
    }

    class ScalaModule2 extends AbstractModule {
      @Override
      protected def configure() {
        bind(classOf[AService]).to(classOf[SomeOtherService])
      }
    }

    val injector = Guice.createInjector(new ScalaModule)
    val component = injector.getInstance(classOf[MyComponent])
    assertEquals("someService", component.callTheService)

    val injector2 = Guice.createInjector(new ScalaModule2)
    val component2 = injector2.getInstance(classOf[MyComponent])
    assertEquals("someOtherService", component2.callTheService)
  }
</pre>

So let&#8217;s explore the test a bit. I&#8217;m using Scala to build a JUnit test, as shown by the annotation on line 1. One of the advantages of this is that it&#8217;s easy to use Scala&#8217;s namespace capabilities to build test classes that are only visible within the test itself, which is what I&#8217;m doing starting line 3. I create a class call ScalaModule with extends Guice&#8217;s base class AbstractModule. I override one method called &#8220;configure&#8221;, which sets up the bindings of interfaces to implementations for this Guice module. (This is all covered in detail in Guice&#8217;s doc).

On line 6 I bind the interface &#8220;AService&#8221; to an implementation of AService called &#8220;SomeService&#8221;. Here&#8217;s what they look like (these classes are defined later in the file &#8211; I don&#8217;t embed them inside the test class as Guice didn&#8217;t let me).

Here&#8217;s the trait for the service:

<pre class="brush:scala">trait AService {
  def service: String
}
</pre>

And a simple implementation:

<pre class="brush:scala">class SomeService extends AService {
  def service(): String = "someService"
}
</pre>

Now I have a component that uses that service, called MyComponent. It looks like this:

<pre class="brush:scala">class MyComponent @Inject()(val service: AService) {
  def callTheService(): String = service.service
}
</pre>

Note the annotation on the first line. This is how you put an annotation on the constructor in Scala, Annoyingly, the () is apparently required. This Inject annotation indicates that when this component is requested from Guice, it should have the appropriate implementation of Service injected.

So now to return to our test, on line 10 you&#8217;ll see we are building a second module, this time binding the AService interface (trait, actually) to the SomeOtherService implementation, which looks like this:

<pre class="brush:scala">class SomeOtherService extends AService {
  def service(): String = "someOtherService"
}
</pre>

Then we get into the meat of the test in line 17. First, we ask Guice for our injector, the &#8220;god object&#8221; for Guice, from which you get all the other object you&#8217;ll need. In the first case, we use our ScalaModule class. Then we ask this injector for our component, and it constructs the component for us, injecting the dependency as necessary. In this situation, we have not told Guice that MyComponent is a singleton (we&#8217;ll deal with that later &#8211; in several different ways), so it builds a new one for us every time.

On line 18, we make the assertion that proves that our MyComponent instance has in fact been built with the &#8220;SomeService&#8221; instance, as opposed to any other instance, by verifying our string that SomeService responds with.

Then we do the whole thing again, except this time asking for the ScalaModule2. ScalaModule2 is where we have the SomeOtherService implementation of AService wired up, so when we assert on line 23, we now see the &#8220;someOtherService&#8221; string returned instead, which means that we&#8217;re properly wired, as expected.

Now let&#8217;s give Guice a little harder work, exploring some scenarios we&#8217;ll see in more sophisticated applications.

In many situations, we&#8217;ll want to avoid creating a new instance of our service object every time we use it. There are a couple of ways to do this with Guice.

<pre class="brush:scala">@Test
  def instanceBindingExample {
    // if you want to bind to a specific instance of a class...
    class InstanceExampleModule extends AbstractModule {
      @Override
      protected def configure() {
        val instance1 = new InstanceService("instance1")
        bind(classOf[AService]).toInstance(instance1)
      }
    }
    val injector = Guice.createInjector(new InstanceExampleModule)
    val service = injector.getInstance(classOf[AService])
    assertEquals("instance1", service.service)
  }
</pre>

In the code above, we&#8217;re configuring our module, called InstanceExampleModule, with a binding that specifies our AService trait uses a specific instance of the class called InstanceService. 

Here&#8217;s InstanceService:

<pre class="brush:scala">class InstanceService(val value: String) extends AService {
  def service(): String = value
}
</pre>

Back in our test, line 13 ensures that we&#8217;re actually talking to the right service, as we fed the service it&#8217;s return string (&#8220;instance1&#8243;) when it was created in the module.

Ok, so now we can inject services, and specify an instance of a service instead of a newly-created one every time. That&#8217;s a good start, but we want to do more.

What if we have to do some more work to instantiate our singleton instance? E.g. what happens if it takes a whole method to create the service?

Guice has that covered as well, like so:<pre class="brush:scala> @Test def providesBindingExample { // if it takes a method to figure out how to invoke a component, you can annotate that method with @Provides // and put it in the module class ProvidedExampleModule extends AbstractModule { @Override protected def configure() { } @Provides def provideAService: AService = new InstanceService("providedInstance") } val injector = Guice.createInjector(new ProvidedExampleModule) val service = injector.getInstance(classOf[AService]) assertEquals("providedInstance", service.service) } </pre> 

Here you see a new module being built, but this time we don&#8217;t actually say anything in the &#8220;configure&#8221; method. Instead, we annotate another method in the module with the @Provides annotation &#8211; this means to Guice &#8220;whenever you need a thing of the type this method returns, call this method&#8221;. Then we verify that that&#8217;s in fact what&#8217;s happening by creating the injector and asking for the service.

Ok, so now we can create instances of services however we want, but we&#8217;ve still only created a single instance of a given trait. What if we&#8217;ve got a whole whack of services that implement our interface? Ok, that&#8217;s also easy:

<pre class="brush:scala">@Test
  def bindingWithNameAnnotationExample {
    // what if I have two implementations of the same interface, how do I say which one I want?
    class ScalaModule extends AbstractModule {
      @Override
      protected def configure() {
        bind(classOf[AService]).annotatedWith(Names.named("foo")).to(classOf[SomeServiceNamedFoo])
        bind(classOf[AService]).annotatedWith(Names.named("bar")).to(classOf[SomeServiceNamedBar])
      }
    }

    val injector = Guice.createInjector(new ScalaModule)
    val barComponent = injector.getInstance(classOf[MyBarComponent])
    val fooComponent = injector.getInstance(classOf[MyFooComponent])
    assertEquals("bar", barComponent.callTheService)
    assertEquals("foo", fooComponent.callTheService)
  }
</pre>

Now we&#8217;ve got a couple of services to declare:

<pre class="brush:scala">class SomeServiceNamedFoo extends AService {
  def service(): String = "foo"
}
class SomeServiceNamedBar extends AService {
  def service(): String = "bar"
}
</pre>

The services themselves both implement our trait, of course, but now we have two different components, one which needs the Foo service, other other one needs the Bar:

<pre class="brush:scala">class SomeServiceNamedFoo extends AService {
  def service(): String = "foo"
}
class SomeServiceNamedBar extends AService {
  def service(): String = "bar"
}
</pre>

In our test, you can see we ask the injector for the two components. What&#8217;s very interesting to me is that **the component themselves are not listed in the module**. Why that&#8217;s important is that unlike Spring (to pick an example many people know), you don&#8217;t need any configuration provided at all for stuff that Guice can work out on it&#8217;s own. This is a good thing.

Anyway, you can see by our asserts that in this situation the Foo service gets the Foo implementation of the AService (SomeServiceNamedFoo), and the Bar service gets SomeServiceNamedBar instead.

Now that we can handle multiple implementations, let&#8217;s go back and consider the singleton vs. new instance issue from another angle: Scala has no concept of the idea of &#8220;static&#8221; classes, but it does have companion objects, which are, in all cases I&#8217;ve seen, better.

If we declare a service like so:

<pre class="brush:scala">object SingletonService extends AService {
  def service(): String = "singleton"
}
</pre>

and another (non-singleton) implementation, like so:

<pre class="brush:scala">class NonSingletonService extends AService {
  def service(): String = "nonsingleton"
}
</pre>

Now we can write a test that tries this out like so:

<pre class="brush:scala">@Test
  def singletonOrPrototype {
    class ScalaModuleSingleton extends AbstractModule {
      @Override
      protected def configure() {
        bind(classOf[AService]).toInstance(SingletonService)
      }
    }

    class ScalaModuleNonSingleton extends AbstractModule {
      @Override
      protected def configure() {
        bind(classOf[AService]).to(classOf[NonSingletonService])
      }
    }

    val singletonInjector = Guice.createInjector(new ScalaModuleSingleton)
    val singleton = singletonInjector.getInstance(classOf[AService])
    assertEquals("singleton", singleton.service)
    val secondInstance = singletonInjector.getInstance(classOf[AService])
    assertSame(singleton, secondInstance)

    val nonSingletonInjector = Guice.createInjector(new ScalaModuleNonSingleton)
    val nonsingleton = nonSingletonInjector.getInstance(classOf[AService])
    assertEquals("nonsingleton", nonsingleton.service)
    val secondNonSingletonInstance = nonSingletonInjector.getInstance(classOf[AService])
    assertNotSame(nonsingleton, secondNonSingletonInstance)
  }
</pre>

The money here comes at the line that binds the classOf[AService] to a singleton &#8211; in this case, the SingletonService. This isn&#8217;t a class, so we don&#8217;t use to(classOf[SingletonService]), we say toInstance(SingletonService) instead.

As you can see from the test, this works very nicely, and gives us a much more Scala-canonical way to do singleton.

However, there are times when we want to declare a regular Scala class, and have Guice only instantiate one of em for us, and handle it as a singleton that way (some examples might be when we&#8217;re using a constructor to inject other dependencies &#8211; although we can use field injection for this, which we&#8217;ll look at later).

We can annotate our class explicitly to tell Guice it&#8217;s a singleton like so:

<pre class="brush:scala">@com.google.inject.Singleton class SingletonClassService extends AService {
  def service(): String = "singletonClass"
}
</pre>

Now we can write a test like so to prove that we get the same instance of our service, even if we ask the injector for it multiples times:

<pre class="brush:scala">@Test
  def singletonClassExample {
    class ScalaModuleSingleton extends AbstractModule {
      @Override
      protected def configure() {
        bind(classOf[AService]).to(classOf[SingletonClassService])
      }
    }

    val singletonInjector = Guice.createInjector(new ScalaModuleSingleton)
    val singleton = singletonInjector.getInstance(classOf[AService])
    assertEquals("singletonClass", singleton.service)
    val secondInstance = singletonInjector.getInstance(classOf[AService])
    assertSame(singleton, secondInstance)
  }
</pre>

The assertSame in JUnit asserts that we have the exact same instance of an object, not that they&#8217;re only equal.

One last scenario: What is the service isn&#8217;t the singleton, but the component is? E.g. what if we have an object instead of class that needs a service injected into it? Turns out Guice can handle that nicely as well. The only extra work we need is to define a trait for the binding of our component, like so, with the service injected into the object:

<pre class="brush:scala">trait SingletonComponentInterface {
  def callTheService:String
}
object SingletonComponent extends SingletonComponentInterface {
  @Inject val service:AService = null
  def callTheService(): String = service.service
}
</pre>

Now we can write a test to make sure this is doing what we want:

<pre class="brush:scala">@Test
  def injectIntoSingletonExample {
    // if you want to inject into an object instead of a class
    class InstanceExampleModule extends AbstractModule {
      @Override
      protected def configure() {
        val instance1 = new InstanceService("instance1")
        bind(classOf[AService]).toInstance(instance1)
        bind(classOf[SingletonComponentInterface]).toInstance(SingletonComponent)
      }
    }
    val injector = Guice.createInjector(new InstanceExampleModule)
    val component = injector.getInstance(classOf[SingletonComponentInterface])
    assertEquals("instance1", component.callTheService)
  }
</pre>

That&#8217;s it for my experiments so far. Here&#8217;s my conclusions, please comment with your experiences:

## The Good, The Bad, and the Ugly

**The Good**  
There was a lot I liked about Guice in Scala. First, no XML was injured in the making of these examples &#8211; everything was code, and fully type-safe (I mentioned it was Scala, right?) I always find myself writing a &#8220;smoke test&#8221; for my Spring apps to verify I haven&#8217;t made a typo in my &#8220;beans.xml&#8221; file &#8211; here I didn&#8217;t need to. Yes, I know you can do XML-free Spring as well, but it&#8217;s the norm with Guice, and it feels a lot lighter weight.

I don&#8217;t need to configure anything for classes that just get injected. This means that the configuration I **do** need to write is very short, and because it&#8217;s a class, it&#8217;s extensible. In my &#8220;real&#8221; project, for instance, I was able to write a module that created services that use static lists for their data (instead of reading and writing to a real database, for instance), then extend that class with an OSGi-aware version that used the &#8220;real&#8221; services from other modules. No repeated work, no wiring, no config &#8211; it just worked.

Auto-handling of singletons, both with companion objects and classes, as I prefer: It was nice to be able to write Scala in a very Scala-like way, and just have the DI framework slot right in whichever way I needed it to, as described above.

**The Bad**  
I have to annotate my classes with Guice-specific annotations, although there is a JSR on the way to standardize these, which makes it a bit less objectionable. What happens if I need to inject to a class I don&#8217;t have source for (e.g. something in an existing Java library that I&#8217;m calling? I also haven&#8217;t tried this in a Servlet environment, although I understand there&#8217;s a Guice extension for that, so I don&#8217;t expect any trouble there.

**The Ugly**  
I have to (it seems) use the @Inject() format, not just @Inject, and I have to insert it in what looks like an odd place in the declaration. Not a big deal, and I suspect I&#8217;ll get used to it.

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

 [1]: http://jonasboner.com/2008/10/06/real-world-scala-dependency-injection-di.html
 [2]: http://code.google.com/p/google-guice/