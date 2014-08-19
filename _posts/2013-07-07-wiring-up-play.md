---
title: Wiring Up Play
author: mnash
excerpt: 'The Play framework recently added support for constructing controllers with dependency injection - we look at the options and techniques for doing so'
layout: post
permalink: /wiring-up-play/
livefyre_version:
  - 3
categories:
  - Scala
  - Software Design
---
The Play Framework is quite a capable tool for creating web applications and RESTful services, but there are a few nuances that didn&#8217;t fit my normal patterns of development.

One of these is the singleton pattern used for the controllers in Play. The default pattern is to use an object, but of course objects don&#8217;t have constructors, so dependency injection isn&#8217;t possible. You can of course simply write code that grabs the necessary dependencies, but that couples the controller to the other classes directly, and makes testing and changing code harder than it needs to be.

This is what it looks like:

<pre class="prettyprint lang-scala linenumstrigger linenums dontquote" skin="sons-of-obsidian">package controllers

import play._
import play.mvc._
    
object Catalog extends Controller {
 val productService = Global.injector.getInstance(classOf[ProductService])

 def listProducts = Action {
    implicit request =&gt;
      Ok(views.html.catalog(productService.list))
  }
}
</pre>

Fortunately, in more recent versions of Play, there&#8217;s a way to use a class instead of an object, and to use the constructor of that class to inject the necessary dependencies.

Here&#8217;s the controller showing the product service being injected instead of accessed externally:

<pre class="prettyprint lang-java linenumstrigger linenums">package controllers

import play._
import play.mvc._
    
class Catalog(productService: ProductService) extends Controller {

 def listProduces = Action {
    implicit request =&gt;
      Ok(views.html.catalog(productService.list))
  }
}
</pre>

Now the controller doesn&#8217;t have any knowledge of how the product service is constructed &#8211; so we can hand in a different one for tests, for example. This is better decoupling. Notice that the controller is now a class, not an object.

Now we need a way to create the initial instances of all of the necessary dependencies when the application starts up. In the case of controllers, we want them to be singletons: that is, there should be only one instance of the 

This is accomplished with Play&#8217;s Global class: it has a method that allows Play to request each controller instance it needs, this method then instantiates the returns the instance as required &#8211; returning the same instance every time.

<pre class="prettyprint long-scala linenumstrigger linenums">package infrastructure

import play.api.GlobalSettings
import scala.slick.session.{Database, Session}
import javax.sql.DataSource
import controllers._
import infrastructure.datastore._

object Global extends GlobalSettings {
  def datastore = {
    val dbSuffix = System.getProperty("db", "mem:testdb")
    val dbUrl = s"jdbc:hsqldb:$dbSuffix"

    import com.jolbox.bonecp.BoneCPDataSource
  
    val ds = new BoneCPDataSource
    ds.setDriverClass("org.hsqldb.jdbc.JDBCDriver")
    ds.setJdbcUrl(dbUrl)
    ds.setAcquireIncrement(5)
    ds
  }

  lazy val productService = new ProductService(dataStore)  
  lazy val catalogController = new Catalog(productService)

  override def getControllerInstance[A](clazz: Class[A]) = {
    case x if x.isAssignableFrom(classOf[Catalog]) =&gt; catalogController.asInstanceOf[A]
    case unk =&gt; throw new IllegalArgumentException(s"Unknown controller ${unk.getClass}")
  }
}
</pre>

You can of course just create the classes manually as needed, as shown above, but there are a few conveniences that can make the process easier.

### Guice

One way is to use [Google Guice.][1]

<pre class="prettyprint lang-scala linenumstrigger linenums">package infrastructure

import com.google.inject.{AbstractModule, Guice}
import domain._
import datastore.Schema
import play.api.GlobalSettings
import scala.slick.session.{Database, Session}
import javax.sql.DataSource
import controllers._
import infrastructure.datastore._

object Global extends GlobalSettings {
  val injector = Guice.createInjector(new CatalogModule)
  injector.getInstance(classOf[DecisionRepository]).generateSampleData
  
  override def getControllerInstance[A](controllerClass: Class[A]) = {
    injector.getInstance(controllerClass)
  }
}

class CatalogModule extends AbstractModule {
def datastore = {
    val dbSuffix = System.getProperty("db", "mem:testdb")
    val dbUrl = s"jdbc:hsqldb:$dbSuffix"

    import com.jolbox.bonecp.BoneCPDataSource
  
    val ds = new BoneCPDataSource
    ds.setDriverClass("org.hsqldb.jdbc.JDBCDriver")
    ds.setJdbcUrl(dbUrl)
    ds.setAcquireIncrement(5)
    ds
  }

  override def configure() {
    bind(classOf[DataSource]).toInstance(dataStore)
    bind(classOf[Database]).toInstance(Database.forURL(dbUrl))
  }
}
</pre>

Using Guice, we also have to annotate the class constructors for the classes Guice instantiates (or use other methods in the Guice module to define which constructor to use, as I generally prefer to avoid the annotations in the classes, as I&#8217;m then coupling my controllers to Guice).

### MacWire

Recently I&#8217;ve been working with [a more Scala-like alternative: MacWire][2]. It uses Macros instead of reflection to produce the necessary injection code at compile-time. It has the advantage of compile-time checking: if a dependency cannot be resolved, the app simply won&#8217;t compile.

(I&#8217;ve omitted the imports for brevity, they&#8217;re the same as above examples)

<pre class="prettyprint lang-scala linenumstrigger linenums">object Global extends GlobalSettings {
  val module = new CatalogModule
  
  override def getControllerInstance[A](classRef: Class[A]) = module.getController(classRef)
}

class CatalogModule {
  import com.softwaremill.macwire.MacwireMacros._

  val datastore = {
    // same as previous examples
  }

  lazy val catalog = wire[Catalog]
  lazy val userRepository = wire[UserRepository]
  lazy val userDataStore = wire[UserDataStore]
  lazy val productService = wire[ProductService]
  lazy val catalogController = wire[Catalog]
  
  def getController[A](classRef: Class[A]): A = classRef match {
    case x if x.isAssignableFrom(classOf[Catalog]) =&gt; catalogController
  }
}
</pre>

I haven&#8217;t worked with MacWire for long, but it looks like it may be a cleaner way to go for more sophisticated applications.

If you&#8217;ve found other ways to approach this issue, please drop me a line and let me know!

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

 [1]: https://code.google.com/p/google-guice/
 [2]: https://github.com/adamw/macwire