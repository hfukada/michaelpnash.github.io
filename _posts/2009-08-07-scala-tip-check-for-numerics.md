---
title: 'Scala Tip: Check for Numerics'
author: mnash
layout: post
permalink: /scala-tip-check-for-numerics/
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
  - command-line
  - numeric
  - Scala
  - testing
---
A colleague the other day need to write a test that checked a string to ensure it was all digits, and happened to be using Scala for it.

An initial thought was to just iterate through the string character by character &#8211; but that was laborious and verbose&#8230;

A second thought was to just try to convert the string to an integer with toInt, then watch for the exception when it wasn&#8217;t, but even this seemed a bit heavy-handed, now that we&#8217;re getting used to Scala&#8217;s expressiveness.

After a quick experiment we came up with a cleaner solution: Use the built-in abilities to convert the string to a list, then use a partially applied function to filter the list, then take the length of the resulting all-digits string. If this length is not the same as the length of the original string, then there are non-digit characters in the string &#8211; otherwise, it&#8217;s all digits.

Here&#8217;s a transcript of a Scala command-line session trying this out:

<div class="capsule" style="text-align: left">
  <pre>
&lt;code&gt;
scala&gt; "foo".toList.filter(_.isDigit).length
res5: Int = 0

scala&gt; "123".toList.filter(_.isDigit).length
res6: Int = 3

scala&gt; "abc123".toList.filter(_.isDigit).length
res7: Int = 3
</pre>
  
  <p>
    </code> </div> <p>
      Of course, you can turn this into a test easily enough by
    </p>
    
    <div class="capsule" style="text-align: left">
      <pre>
&lt;code&gt;
assertEquals(originalString.length, originalString.toList.filter(_.isDigit).length)
&lt;/code&gt;
</pre>
      
      <p>
        Now that's pretty concise <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Scala Tip: Check for Numerics" class="wp-smiley" title="Scala Tip: Check for Numerics" />
      </p>
      
      <div class="g-plusone" data-annotation="inline" data-width="300">
      </div>
      
      <p>
        <!-- Place this tag after the last +1 button tag. -->
        
        <br />
      </p>
      
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