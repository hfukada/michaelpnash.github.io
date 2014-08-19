---
title: Slick and Play
author: mnash
excerpt: "Slick and Play work great together, but using them with multiple databases and connection pooling takes a couple of small tricks. In this post, I'll show how I've done this in my applications."
layout: post
permalink: /slick-and-play/
livefyre_version:
  - 3
categories:
  - Scala
tags:
  - BoneCP
  - Hsqldb
  - Play
  - Postgres
  - Scala
---
In building a few applications with <a href="http://slick.typesafe.com/" target="_new">Slick</a> and <a href="http://www.playframework.com/" target="_new">Play</a>, I was very pleased by how easily Slick integrates with Play: the framework makes no assumptions at all about what kind of database interaction you&#8217;re going to use, so there&#8217;s nothing to bypass, you just get slick on the classpath and use Slick however you&#8217;d like to.

Here&#8217;s an example from one of my applications that&#8217;s using Slick:

<pre class="prettyprint lang-scala linenumstrigger linenums">import sbt._
import sbt._
import play.Project._

object ApplicationBuild extends Build {

  val appName         = "example"
  val appVersion      = "1.0"

  val appDependencies = Seq("com.typesafe.slick" %% "slick" % "1.0.0",
    "org.scalatest" %% "scalatest" % "2.0.M5b" % "test",
    "com.typesafe" %% "scalalogging-slf4j" % "1.0.1",
    "com.jolbox" % "bonecp" % "0.7.1.RELEASE",
    "com.softwaremill.macwire" %% "core" % "0.1"
  )
  
  val main = play.Project(appName, appVersion, appDependencies).settings(
    sbt.Keys.fork in Test := false
  )
}
</pre>

Two small areas were not immediately obvious, though, and took a bit of tinkering. Slick does not prescribe any particular form of connection pooling, so you must add your own. This is a must for any kind of serious production application, IMO, but it&#8217;s quite easy to do.

The second issue was database-independance: Although Slick is not database-specific, the drivers you use to do lifted mapping are, unless you take a few simple steps (one of which has a small Gotcha) to ensure you&#8217;re not tied to a specific database.

As I like to use [Hypersonic SQL][1] for my testing database, but often select [Postgres][2] for my deploy database, I switch databases a lot.

Below I&#8217;ll describe how I handled both these issues.

## Connection Pooling

In one of our apps that did a lot of small database operations we found a six-times performance boost just by adding connection pooling, so it&#8217;s a must for production deploys, I think.

The preferred choice for connection pooling in Play appears to be <a href="http://jolbox.com/" target="_new">BoneCP</a>, although I&#8217;ve successfully used [C3PO][3] as well.

For BoneCP, the setup of a data source is pretty straightforward:

<pre class="prettyprint lang-scala linenumstrigger linenums">lazy val datasource = {
    val dbSuffix = System.getProperty("db", "mem:testdb")
    val dbUrl = s"jdbc:hsqldb:$dbSuffix"

    import com.jolbox.bonecp.BoneCPDataSource

    val ds = new BoneCPDataSource
    ds.setDriverClass("org.hsqldb.jdbc.JDBCDriver")
    ds.setJdbcUrl(dbUrl)
    ds.setAcquireIncrement(5)
    ds
  }
</pre>

There are many other options you can configure, and the BoneCP documentation enumerates them.

## Multiple Database Types

Allowing Slick to easy switch between databases is slightly trickier (at the moment in any case), but not that hard. 

Here&#8217;s a simple class that accesses Customer records, defined in a Schema class, with DTO object called CustomerDTO (the case class corresponding to a row in the database table).

<pre class="prettyprint lang-scala linenumstrigger linenums">package infrastructure.datastore
import scala.slick.jdbc.{GetResult, StaticQuery}
import scala.slick.jdbc.StaticQuery.interpolation
import scala.slick.driver.ExtendedDriver
import slick.session.{Session, Database}
import Schema._
import java.util.UUID
import javax.sql.DataSource

class CustomerDataStore(driver: ExtendedDriver, dataSource: DataSource) {
  import driver.simple._
  import driver.DeleteInvoker
  implicit val session = database.createSession
  
 implicit def session(dataSource: DataSource): Session = Database.forDataSource(dataSource).createSession

  def insert(dto: CustomerDTO) = Customers.insert(dto)

  def findByCustomerCode(code: String): List[CustomerDTO] = Query(Customers).filter(_.customerCode === code.bind).list

  def clear(implicit session: Session) { new DeleteInvoker(Query(Customers)).delete }
}
</pre>

In the above code the only tricky bit is the definition of &#8220;clear&#8221; &#8211; it must use the DeleteInvoker due to an oddity in the way Slick&#8217;s implicits work for the database-independent drivers &#8211; if you were using only a single driver, the clear method is slightly simpler.

Now at startup, we simply pass the appropriate driver to the CustomerDataStore class when it&#8217;s instantiated. We can specify the type of database using a system property or some other config value (a string &#8220;dbType&#8221; in the following example), like so:

<pre class="prettyprint lang-scala linenumstrigger linenums">private def driver: ExtendedDriver =
  dbType match {
    case "hsql" =&gt; HsqldbDriver
    case "mssql" =&gt; SQLServerDriver
    case _ =&gt; throw new IllegalArgumentException("dbType property must be either hsql or mssql")
  }
</pre>

Then we hand the &#8220;driver&#8221; and our previously-defined &#8220;datasource&#8221; as the constructor parameters to our CustomerDataStore class:

<pre class="prettyprint lang-scala linenumstrigger linenums">lazy val customerDataStore = new CustomerDataStore(driver, dataSource)
</pre>

Of course, if we&#8217;re <a href="http://jglobal.com/wiring-up-play/" target="_new">using something like MacWire to do our dependency injection</a>, this can be simplified to 

<pre class="prettyprint lang-scala linenumstrigger linenums">lazy val customerDataStore = wire[CustomerDataStore]
</pre>

With these couple of tricks, you&#8217;ve got Slick wired up to use any database type you need (that it supports, which is quite a few), and you get a substantial boost in overall performance with the use of connection pooling!

<div class="g-plusone" data-annotation="inline" data-width="300">
</div>

<!-- Place this tag after the last +1 button tag. -->

  


<div class="st-callout hastitle lightblue center" >
  <h4 class="st-callout-title ">
    Principles and Practices
  </h4>
  
  <div class="inside">
    <i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book (almost finished!): <a href="http://jglobal.com/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="http://jglobal.com/dispatches/">Craftsmanship Dispatches</a> newsletter.
  </div>
</div>

<div class="clear">
</div>

 [1]: http://hsqldb.org/
 [2]: http://www.postgresql.org/
 [3]: http://www.mchange.com/projects/c3p0/