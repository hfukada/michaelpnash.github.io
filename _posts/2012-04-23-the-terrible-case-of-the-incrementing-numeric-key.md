---
title: The Terrible Case of the Incrementing Numeric Key
author: mnash
excerpt: Incrementing numeric keys can be a horrible mistake, limiting future changes of software.
layout: post
permalink: /the-terrible-case-of-the-incrementing-numeric-key/
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
  - Software Craftsmanship
---
I&#8217;ve recently had a chance to get kicked again in a place I&#8217;d rather not get kicked by one of the many horrible side-effects of an incrementing numeric key.

This has made me want to once again rant and rave about the many negative attributes of this pattern. Instead, I&#8217;m going to slow down and try to enumerate them more clearly <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile The Terrible Case of the Incrementing Numeric Key" class="wp-smiley" title="The Terrible Case of the Incrementing Numeric Key" /> 

First, let&#8217;s examine what pattern we&#8217;re talking about: In it&#8217;s most common form, it is the pattern of assigning an incrementing numeric value as the synthetic key to a persistent entity of some sort, often in a relational database. One of the reasons it&#8217;s often found in relational databases is that it&#8217;s easy: many databases provide an automatic facility for assigning incrementing numeric keys to a table.

I won&#8217;t even go near the debate of synthetic keys vs. natural keys for persistence, so I won&#8217;t count that for or against incrementing numeric keys.

**Can&#8217;t be easily distributed**  
A huge flaw in incrementing numeric keys is that their assignment is, by definition, not distributable without taking special steps. Even if the database in question is assigning the keys for you, all new records must be inserted into the same instance of the database to ensure duplicates are not assigned.

Incrementing numeric keys also don&#8217;t shard well, as their distribution is completely predictable, causing some problems with large datasets that are avoided with other more easily hashable types of keys.

**Single point of contention**  
Whether it be a database or the infamous &#8220;next number table&#8221;, the place where the key is assigned with an incrementing key is a point of contention, something any scalable system wants to avoid at all costs.

**Implies order, but doesn&#8217;t make it explicit**  
An incrementing key implies sequence or order, but does not explicitly define order. That is, if you sort the entries by the key, they are (supposedly) in order of insertion. The key isn&#8217;t meant for this, however, and it is far better to use an actual meaningful order, such as a created date/time stamp or other sequence that actually has a purpose in the domain model.

**Temptation to assign meaning**  
The most insidious problem with an incrementing numeric key is that it is often too tempting to assign meaning to the key, where none actually exists. If the key is supposed to be a meaningless unique identifier, then use a meaningless unique identifier, not an easily recognized incrementing value that will tempt users of the data (if you expose the key &#8211; arguably a second problem) to infer &#8220;ah, this number is greater than 1000, therefore this record was inserted after June the 12th&#8221;, or, worse, setting a new starting point in the number for a certain class of data &#8220;keys greater than 1000000 are created by customers, less than 1000000 are created by the system&#8221;. I&#8217;ve seen every kind of crazy variation of this kind of thing, and they&#8217;re all trouble, and none of them could have happened with a nice incomprehensible GUID instead of an incrementing numeric id.

**Fixed Size**  
While it is entirely possible to set an incrementing numeric key to a reasonable size, allow for all possible expansion, often this is not done. This will frequently lead to that horrible moment in the future where you realize the data set is going to scale much larger than was anticipated, and the key must be resized. Often this happens as a result of a bizarre tendency to want to &#8220;save space&#8221; by trading off a couple of bytes.

To my mind, any *one* of these disadvantages is enough to avoid the trap of the incrementing numeric key, but all of them put together add up to a pattern I&#8217;d most certainly avoid unless there were highly compelling reasons for it, and &#8220;because it&#8217;s easy&#8221; is not a compelling enough reason.

**Alternatives**  
Not one to complain of a problem without presenting some possible solutions, I thought I&#8217;d quickly mention some of the alternatives to the numeric incrementing key:

**Natural Key**  
One way to avoid a synthetic key using a numeric incrementing value is to avoid a synthetic key altogether. If you use a naturally unique value from the data in question as the key, the entire problem goes away &#8211; although, arguably, other problems can arise, but these are outside the scope of this post.

**GUID or ObjectId**  
My favorite solution to the key issue, if a natural key is for some reason not appropriate, is to use a randomly-generated GUID. In the bson libraries supplied with MongoDB&#8217;s driver, the ObjectId value is such a GUID, and generates a 24-character random hexidecimal key. The chance of a collision is vanishingly small, and this value makes an excellent key for both key-value and relational databases.

Java&#8217;s own libraries also provides a GUID-generator, also suitable for the same purpose.

**Conclusion**  
I hope this article gives you a bit of food for thought about numeric incrementing keys, and I encourage you to consider the available alternatives next time this issue comes up in your design work.

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