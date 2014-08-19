---
title: Extending ScalatraFunSuite
author: mnash
excerpt: Testing Scalatra
layout: post
permalink: /extending-scalatrafunsuite/
related_exlink_2:
  - 
related_exlink_1_desc:
  - 
related_exlink_1:
  - 
related_exlink_4:
  - 
related_exlink_3_desc:
  - 
related_exlink_5_desc:
  - 
related_exlink_5:
  - 
related_exlink_4_desc:
  - 
related_exlink_3:
  - 
related_exlink_2_desc:
  - 
categories:
  - Scala
---
I&#8217;ll keep this one very short and to the point: I&#8217;ve been working extensively with Scalatra and Scalate recently, and it&#8217;s been great. My only minor problem has been with the bundles testing capabilities with Scalatra, namely the ScalatraFunSuite.

It lets you very easily test your Scalatra filters or servlets, but the number of things you can assert on is a bit limited. You can check status (to ensure you get a 200 instead of a 404 or a 500, for instance), and you can assert things about the contents of the response body, such as if it contains an expected string. All well and good, but not enough for my test-driven proclivities.

So I did a bit of tinkering, and came up with a nice clean way to grab things such as cookies, response values being passed to the template, the name of the Scalate template being called, and so forth.

I want to be able to write a test like this:

<pre class="brush:scala">test("edit the organization data") {
    get(ORGANIZATION_URL) {
      status should equal(200)
      assert(template.endsWith(OrganizationController.ORGANIZATION_TEMPLATE))
    }
  }
</pre>

For instance, where I assert that the template that got called was a certain template that I expect.

It turns out this isn&#8217;t very hard &#8211; just stick another Filter in the chain when you set up your test, like so:

<pre class="brush:scala">addFilter(classOf[TestFilter], "/*")
   addFilter(new CommonFilter, "/*")
</pre>

And yes, I am using a different method invokation on the second line &#8211; I do this intentionally, so I can control creation of the servlet class under test, as I use Guice-servlet to inject all it&#8217;s service dependencies, and at test-time, I do this with implicit parameter &#8211; but that&#8217;s a whole &#8216;nother post <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Extending ScalatraFunSuite" class="wp-smiley" title="Extending ScalatraFunSuite" /> 

Anyway, TestFilter, as you might imagine, gives me &#8220;hooks&#8221; that I can assert on later. It looks like this:

<pre class="brush:scala">object TestFilter {
  var lastURI: String = null
  var values: Map[String, AnyRef] = Map()
  def template = values("scalateTemplates").asInstanceOf[List[String]].head
  val cookies = ListBuffer[Cookie]()
}

class TestFilter extends Filter {

  def destroy() {}

  def init(conf: FilterConfig) {}

  override def doFilter(request: ServletRequest, response: ServletResponse, filterChain: FilterChain) {
    val wrappedResponse = new ResponseWrapper(response.asInstanceOf[HttpServletResponse])

    val httpRequest = request.asInstanceOf[HttpServletRequest]
    lastURI = httpRequest.getRequestURI
    filterChain.doFilter(request, wrappedResponse);
    val names = httpRequest.getAttributeNames
    while(names.hasMoreElements) {
      val name = names.nextElement.asInstanceOf[String]
      val value = httpRequest.getAttribute(name)
      println(name + ":" + value)
      values += (name -&gt; value)
    }
  }

  class ResponseWrapper(val response: HttpServletResponse) extends HttpServletResponseWrapper(response) {
    override def addCookie(cookie: Cookie) {
      super.addCookie(cookie)
      cookies += cookie
    }
  }
}
</pre>

That&#8217;s all there is to it &#8211; now I can call my servlet under test just like in the first code snippet, and assert on values being sent to the template, on the name of the template, on cookies, and so forth.

That&#8217;s it! Hope this turns out to be useful to some other Scalatra aficionados out there!

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