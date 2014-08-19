---
title: Sustainable Design and Development
author: mnash
layout: post
permalink: /sustainable-design-and-development/
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
  - Software Design
tags:
  - code debt
  - coverage
  - design
  - metrics
  - sustainable
---
No, I don&#8217;t mean design that uses trees and development on green laptops powered by solar panels <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Sustainable Design and Development" class="wp-smiley" title="Sustainable Design and Development" /> 

When I say &#8220;sustainable&#8221; in this context I&#8217;m talking about the ability to keep working on a piece of software over the long term without it becoming so difficult to add new business value that it&#8217;s easier to throw it away and start over, or at the least to refactor very significantly.

When working in an Agile methodology, we mustn&#8217;t think that everything we need to know is contained within the user story we&#8217;re working on. How that story fits into the existing system, how it affects other (existing and new) stories, how it affects system design, performance, maintainability &#8211; these are all factors that professional developers must be keeping in mind as they read a story. We must be ready to relay concerns over possible negative impacts in any of these areas to the story originator, as often there is sufficient flexibility in a story to allow it to be refined so that such concerns are removed. It is our responsibility as software practitioners to ensure that adding a new story doesn&#8217;t reduce our codebase&#8217;s quality, even if it requires work beyond the scope of the story itself.

This is where automated tools to help try to measure some facets of code related to code quality can come in handy: you then have a yardstick to ensure that quality is not heading downhill as new features get added. For instance, if you&#8217;ve got a static analysis tool that measures your cyclomatic complexity, you might set a max limit on that complexity that is not to be exceeded by any new code. Of course, that&#8217;s just one facet, and not every important aspect of software quality can be measured mechanically, but it does provide some assistance to have such tools. Code coverage is another area: if you&#8217;ve established 100% as your target for coverage, then new features should ensure they don&#8217;t violate that.

The trick is to make sure that every new story incorporated into code leaves the code at least as clean as it started, if not better, both from a pure code point of view and from a design point of view. This is of course, a tall order, but one well worth trying to hold to.

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