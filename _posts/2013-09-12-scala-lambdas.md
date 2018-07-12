---
title: Scala Lambdas
author: mnash
excerpt: Scala lambda expressions are often confused with other language features, here we explore and contrast them with closures, with examples of how they can be used.
layout: post
permalink: /scala-lambdas/
categories:
  - Scala
tags:
  - Scala
---
A *lambda* or, more specifically a *lambda expression* is a term used to refer to an expression that does not reference a value or variable, but instead references an anonymous function.

Scala supports the idea of lambda expressions quite nicely, and in several different forms, but it&#8217;s easy to confuse them with other similar constructs, like closures.

## Why?

There are a few reasons most people use lambda expressions:

### Convenience

For a simple function that is used only in one place, a lambda is quicker and easier, and more expressive, than the alternative of declaring a whole function. There are places where a function with a name is more expressive, though, so lambdas shouldn&#8217;t be used when they would obscure intent.

### Decoupling

Passing a lambda can allow different aspects of an application to be more fully decoupled from each other: one component doesn&#8217;t need to know the &#8220;internals&#8221; or names inside some other component, only the signature of the lambda that is to be passed. 

### Reusability

Especially in functional programming, using lambdas can allow us to create highly re-usable pieces of code. A very simple example might be a function that can iterate over a list of objects and apply some transformation to them. The transformation doesn&#8217;t need to be known at compile time, only the signature of the transformation. This means our function can be re-used for any kind of transformation. (Of course, this is too simple an example, as this is pretty much what the map function built in to Scala does, but you get the idea).

## How?

Lambdas in Scala are pretty simple in syntax: they are defined by their function signature. Lets look at this in the Scala REPL:

{% highlight scala %}
scala> (l: Long) => l * l
res0: Long =&gt; Long = &lt;function1&gt;
{% endhighlight %}

The REPL reports correctly that we have defined a function that takes a single Long and returns a Long (in this case, the square of the parameter)

We can put this to use like so:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; val x = (l: Long) =&gt; l * l
x: Long =&gt; Long = &lt;function1&gt;

scala&gt; List(1l, 2l, 3l).map(x)
res2: List[Long] = List(1, 4, 9)
</pre>

Or, more compactly:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; List(1l, 2l, 3l).map((l: Long) =&gt; l * l)
res3: List[Long] = List(1, 4, 9)
</pre>

In this case we&#8217;re declaring the Lambda right inline, which doesn&#8217;t allow the best re-use, but might be more expressive in some cases.

Of course, we can go all the way to the most compact form:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; List(1l, 2l, 3l).map(l =&gt; l * l)
res5: List[Long] = List(1, 4, 9)
</pre>

A lambda can also be used as a parameter to a function, and in this form is much more valuable for decoupling and re-use, like so:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; def transformedSum(original: List[Long], f: (Long) =&gt; Long) = original.map(f).sum
transformedSum: (original: List[Long], f: Long =&gt; Long)Long
</pre>

In this case the &#8220;f&#8221; parameter of transformedSum expects a function that transforms one long into another Long. The function then applies whatever transformation it is told to by &#8220;f&#8221; to each value in a list of Longs, then returns the sum of the result.

We can call the function with different lambdas to change it&#8217;s behaviour easily:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; transformedSum(List(1l, 2l, 3l), (l: Long) =&gt; l * l)
res7: Long = 14
</pre>

Or, with a different lambda:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; transformedSum(List(1l, 2l, 3l), (l: Long) =&gt; l * 2)
res8: Long = 12
</pre>

Or even:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; transformeadSum(List(1l, 2l, 3l), l =&gt; l)
res10: Long = 6
</pre>

## Lambda vs. Closure

While a lambda is essentially the same as a function, taking parameters and returning a value, a closure is a slightly different beast: It &#8220;closes over&#8221; a scope, and may have access to values declared in that scope that are *not* explicitly passed as parameters. 

For example, here&#8217;s a very simple closure in use:

<pre class="prettyprint lang-scala linenumstrigger linenums">val maxRate = 100
val someValues = List(2, 4, 6, 8, 10)
someValues.map(value =&gt; {
  val factor = computeFactor(value)
  callSomeOtherThing(value, maxRate)
})
</pre>

The closure is everything from the open brace in the &#8220;map&#8221; line to the close brace. As you can see, the value of &#8220;maxRate&#8221;, defined outside the closure, is used *inside* the closure &#8211; a key difference.

A closure, therefore, might be only valid in a specific context, whereas a lambda or anonymous function can be reused without regard to the context, as everything it needs to know to do it&#8217;s business is passed in as parameters.

## Scala Lambdas

As you can see from this very quick introduction, lambdas can be applied in many different ways in Scala &#8211; we&#8217;ve only touched on a few here. They can also make testing and refactoring easier, and allow mocks or stubs to be easily created for test-time, but that&#8217;s another post <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Scala Lambdas" class="wp-smiley" title="Scala Lambdas" /> 

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
