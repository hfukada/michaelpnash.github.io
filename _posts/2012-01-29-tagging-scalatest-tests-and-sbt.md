---
title: Tagging ScalaTest Tests and SBT
author: mnash
excerpt: "When you're writing tests, you may have occasion to segregate some tests from the others - perhaps your functional tests, integration tests, or ui tests, or just tests that run more slowly than the rest of your suite."
layout: post
permalink: /tagging-scalatest-tests-and-sbt/
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
  - sbt
  - Scala
  - scalatest
  - xsbt
---
I want to share a trick for a combination I suspect a number of people are using: SBT and ScalaTest

When you&#8217;re writing tests, you may have occasion to segregate some tests from the others &#8211; perhaps your functional tests, integration tests, or ui tests, or just tests that run more slowly than the rest of your suite. 

There are a number of ways to tackle this (one good way is with SBT sub-projects, which I&#8217;ll cover in another post), but another option is to &#8220;tag&#8221; your tests. The ScalaTest doc covers [tagging here][1], but what&#8217;s not as clear is how you do this and still run your tests with SBT.

Let&#8217;s say you have tagged some tests with the tag &#8220;Ui&#8221;, so you&#8217;ve got test declarations that look like this:

`<br />
describe("some thing I want to test") {<br />
  it ("should do a thing", Ui) {<br />
    ....<br />
  }<br />
}<br />
`

I only want to run this test (and all other tests tagged &#8220;Ui&#8221;) in one particular job on my CI server.

What I need to do is pass the -l and -n options to ScalaTest, but I want to do this only when a certain system property is passed to my SBT instance. E.g. if I have a property &#8220;ui&#8221;, I can pass it to SBT with &#8220;-Dui=true&#8221;. How do I get this property to set the right option for ScalaTest so that when ui is true, ONLY my Ui-tagged tests run, and when ui is false, all the other tests EXCEPT the Ui-tagged tests run?

Here&#8217;s what I did in my build.sbt file:

`<br />
testOptions in Test ++= (if (System.getProperty("ui", "false") == "false") Seq(Tests.Argument("-oDF"), Tests.Argument("-l"), Tests.Argument("Ui")) else Seq(Tests.Argument("-oDF"), Tests.Argument("-n"), Tests.Argument("Ui")))<br />
`

What this says is that I always want the arguments &#8220;-oDF&#8221; passed to Scalatest, but that when ui is false, I want &#8220;-l Ui&#8221; and when ui is true, I want &#8220;-n Ui&#8221;. I default ui to false, so if it&#8217;s not specified at all, thats the same as false.

Now I can simply set a system property for my Jenkins builds, and the right tests are run at the right time.

I thought this might be helpful to others, as it took a bit of digging to figure out the exact syntax.

Note that this appears only to work with Scalatest 1.7RC1 (or later, probably), and SBT 0.11.2 or later.

 [1]: http://www.scalatest.org/user_guide/tagging_your_tests