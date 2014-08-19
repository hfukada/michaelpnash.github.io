---
title: Scala Vectors
author: mnash
layout: post
permalink: /scala-vectors/
categories:
  - Emacs
  - Scala
tags:
  - Scala
  - Vector
---
The Scala collections library is a rich toolkit, and it takes some time to get used to all it offers. One of those choices are <a href="http://www.scala-lang.org/api/current/index.html#scala.collection.immutable.Vector" target="_new">Scala Vectors</a> &#8211; let&#8217;s examine why it might be good one.

When I first started working with Scala, back in 2.7 days I believe, Vector wasn&#8217;t there, but it was introduced in 2.8, and quickly became one of my favorites in the colection library. It has some efficiency advantages over Lists, that we&#8217;ll explore later, and is, like a list, an immutable sequential collection with all the methods you&#8217;d expect on List and a few more.

<div class="st-callout black center" style="width:50%;" >
  <div class="inside">
    Roger, Roger. What&#8217;s our vector, Victor?<br /> - <i>Captain Oveur</i>
  </div>
</div>

<div class="clear">
</div>

You can create a Vector just like a List, like so:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; val victor = Vector(3, 2, 1)
victor: scala.collection.immutable.Vector[Int] = Vector(3, 2, 1)</pre>

Unlike a list, though, a Vector is indexed, so we can say:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; victor(2)
res1: Int = 1</pre>

If we wanted an index on a list we&#8217;d have to use zipWithIndex to generate it, or turn it into another type (like a Vector!)

You can perform the usual immutable operations, such as returning a vector with new elements appended, such as

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; val crew = Vector("roger", "over") :+ "victor"
crew: scala.collection.immutable.Vector[String] = Vector(roger, over, victor)</pre>

You can also replace one element by index easily:

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; val second = crew.updated(1, "joe")
second: scala.collection.immutable.Vector[String] = Vector(roger, joe, victor)</pre>

Which would be a bit trickier with a list.

## Efficient

Vector also has the advantage of generally being faster and more efficient with RAM than a plain List. If you use a Seq, you&#8217;ve probably already used a Vector &#8211; it&#8217;s the default implementation of a Seq.

## Abstract

The Vector is also slightly more abstract than List, in the sense that we are saying we have a collection with a specific order and a finite length, I&#8217;m not ensuring that I can only do full traversals (such as with a list).

There&#8217;s the usual huge list of operations available on Vector, even more than on list. If we ask the REPL (by hitting &#8220;tab&#8221; after the dot):

<pre class="prettyprint lang-scala linenumstrigger linenums">scala&gt; victor.
++                   ++:                  +:                   /:                   /:                  :+                   :                   addString            
aggregate            andThen              apply                applyOrElse          asInstanceOf         canEqual             collect              collectFirst         
combinations         companion            compose              contains             containsSlice        copyToArray          copyToBuffer         corresponds          
count                diff                 distinct             drop                 dropRight            dropWhile            endsWith             exists               
filter               filterNot            find                 flatMap              flatten              fold                 foldLeft             foldRight            
forall               foreach              genericBuilder       groupBy              grouped              hasDefiniteSize      head                 headOption           
indexOf              indexOfSlice         indexWhere           indices              init                 inits                intersect            isDefinedAt          
isEmpty              isInstanceOf         isTraversableAgain   iterator             last                 lastIndexOf          lastIndexOfSlice     lastIndexWhere       
lastOption           length               lengthCompare        lift                 map                  max                  maxBy                min                  
minBy                mkString             nonEmpty             orElse               padTo                par                  partition            patch                
permutations         prefixLength         product              reduce               reduceLeft           reduceLeftOption     reduceOption         reduceRight          
reduceRightOption    repr                 reverse              reverseIterator      reverseMap           runWith              sameElements         scan                 
scanLeft             scanRight            segmentLength        seq                  size                 slice                sliding              sortBy               
sortWith             sorted               span                 splitAt              startsWith           stringPrefix         sum                  tail                 
tails                take                 takeRight            takeWhile            to                   toArray              toBuffer             toIndexedSeq         
toIterable           toIterator           toList               toMap                toSeq                toSet                toStream             toString             
toTraversable        toVector             transpose            union                unzip                unzip3               updated              view                 
withFilter           zip                  zipAll               zipWithIndex</pre>

So, the next time you reach for a collection, consider the humble Vector, it may just be on the course you need!

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