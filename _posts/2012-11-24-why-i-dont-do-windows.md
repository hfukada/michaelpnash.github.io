---
title: 'Why I don&#8217;t do Windows'
author: mnash
excerpt: "I don't work with Microsoft products when I can help it, and I especially avoid Windows. In this article I describe why."
layout: post
permalink: /why-i-dont-do-windows/
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
<p>A point of humor among people I&#8217;ve worked with over the years is my well-known dislike for anything produced by Microsoft, especially their operating systems.</p>
<p>While it may get a chuckle from those who know me, I&#8217;m quite serious in my dislike for Windows and it&#8217;s kin, and I like to believe I have good reasons for it. Every now and then I get the serious question, why don&#8217;t I work with Windows, or Microsoft products in general, so I thought I&#8217;d collect my answers, then I can just point people here when it comes up again.</p>
<p>I didn&#8217;t just wake up one day and decide I didn&#8217;t want to work with Windows, it&#8217;s been a long-standing decision on my part for a great many reasons, all of them experience-based. Its not like I don&#8217;t <b>know</b> Windows, although I&#8217;m not familiar with several of it&#8217;s most recent incarnations. Back in the day I worked extensively with Windows and it&#8217;s ancestor MS-DOS. Fortunately, though, I had initially done most of my work on Unix variants, so I had a basis for comparison. And the comparison was not favorable, to put it mildly. While Windows, thanks in part to Microsoft&#8217;s near-monopoly, was very popular on personal computers, most of my early software development experience is on what I like to characterize as &#8220;real&#8221; computers. That is, systems meant for doing business, for crunching numbers, for making accounts balance. These systems often ran some variant of Unix, as they were intended from the start for multitasking multiuser loads. Even the venerable PDP series from DEC, on which much of what we now call Unix and it&#8217;s ancestors was invented, ran circles around the PC&#8217;s of the day when it came to overall business suitability. Personal computers were fine, if what you wanted to do was write a letter or play a game, but don&#8217;t get them confused with a real computer, which is what you used to do real business.</p>
<p>Now, that may seem like an entirely antiquated viewpoint. Today&#8217;s PC&#8217;s have more power in their graphics and network cards than a PDP-11 had in it&#8217;s central PCU, and my iPhone has more memory in it&#8217;s audio buffer than they had on the whole machine. Very true &#8211; but I&#8217;m still not going to run my business on my iPhone. UI technology has come what we refer to as &#8220;forward&#8221; an entire generation, with GUIs and mice and windows and touch screens and all the rest. Back in the dark ages came a technique known as &#8220;cient-server&#8221;, which was basically where we&#8217;d run the UI bit of an application on a desktop machine, quite often a Windows one, and the actual application logic on a backend machine, very often a Unix one. This technique supplanted the old-fashioned &#8220;dumb terminal&#8221;, which lacked any kind of real GUI support. </p>
<p>Now fast forward 30 years, and &#8230; well, it&#8217;s pretty much the same. We&#8217;ve come full circle, with a web browser in many respects becoming the modern replacement for a &#8220;client&#8221; portion, and the server bit frequently running on a machine in a data center somewhere. What&#8217;s that machine on the back-end running? More often than not, some variant of Unix, or it&#8217;s modern near-successor, Linux.</p>
<p>So how does all this have anything to do with Windows? Well, Windows was born and raised to be a &#8220;desktop&#8221; operating system, even though many ill-fated and ill-advised attempts have been made to pretend it&#8217;s capable of being &#8220;server-class&#8221;, with varying degrees of success. It is tricky to take a system designed for a single interactive user and make it compete with a system whose heritage was expressly designed for heavy concurrent load, time-slicing and context switching, and the management and handling of multiple users. So why do we keep trying? I know why Microsoft keeps trying &#8211; they want a larger slice of that much more lucrative server-side pie. But why do we, the technology professionals, keep aiding and abetting them?</p>
<p>I for one chose not to, long ago. Since that time, many viable alternatives have arisen to Microsoft&#8217;s products even for the desktop, and they are all demonstrably superior to Windows, in virtually every way. Therefore Windows simply doesn&#8217;t make any business sense to me. The ROI isn&#8217;t there, the payback is nowhere to be seen. Every time I&#8217;ve been forced, kicking and screaming, to participate in an effort to put it to real business use, it&#8217;s been either a total or relative failure &#8211; and no, not because I just didn&#8217;t want it to succeed, I don&#8217;t sabotage projects I&#8217;m involved in. I gave it a fair shake, not just once, but many times. I paid the license fees, I paid for all the extra stuff you actually need to make Windows work (virus protection, compilers and IDEs, etc etc), and I stuck it out until we had developed a product that was less stable, less performant, anemically featured and far more expensive than if we&#8217;d just tossed everything Microsoft and started again. Been there, done that, no interest in going back.</p>
<p>Beyond simply having bad technology, Microsoft backs it up with business practices that can best be described as unpalatable, and perhaps more accurately described as illegal, as many major lawsuits over the years can attest. I prefer to deal with organizations for which I have at least a certain level of respect, if not admiration. Microsoft&#8217;s efforts over the years have, in my opinion, seriously interfered with the development of much better software in the entire market, not just for Windows.</p>
<p>Most other counter-arguments take the form of &#8220;yes, it used to suck, but it sucks way less now!&#8221;, which is again not sufficiently compelling for me to absorb the business disadvantages. It&#8217;s all about the latinum, after all, in business.</p>
<p>I&#8217;m quite sure people with a vested interest in their Microsoft-based knowledge will be screaming &#8220;infidel&#8221; by now, telling me that I&#8217;m simply closed-minded, that I don&#8217;t know what I&#8217;m talking about. That may be so. I&#8217;ve only been making a living in the software industry for about three decades, and one thing I know for sure is that I&#8217;ve still got a lot to learn. But one eventually has to make judgments and form opinions when exposed to different technologies over the years, and I relegate all things Microsoft to the same heap as EJB Entity Beans &#8211; an interesting idea with a terrible implementation that I don&#8217;t want anywhere near my business projects. It&#8217;s just not worth it.</p>
<p>In the last few years, its starting to look like a fair chunk of the industry is starting to agree with me, if Microsoft&#8217;s market share is any indication.</p>
<p>For some other opinions on the subject, you may find some of the following interesting reading:</p>
<p><a href="http://www.aaxnet.com/design/msanti.html">Why Not Windows?</a><br />
<a href="http://www.fixedbylinux.com/windows"></p>
<div class="g-plusone" data-annotation="inline" data-width="300"></div>
<p><!-- Place this tag after the last +1 button tag. --><br />
<script type="text/javascript">
  (function() {
    var po = document.createElement('script'); po.type = 'text/javascript'; po.async = true;
    po.src = 'https://apis.google.com/js/plusone.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(po, s);
  })();
</script></p>
<div class="st-callout hastitle lightblue center" >
<h4 class="st-callout-title ">Principles and Practices</h4>
<div class="inside">
<i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book: <a href="http://jglobal.com/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="http://jglobal.com/dispatches/">Craftsmanship Dispatches</a> newsletter.
</div>
</div>
<div class="clear"></div>
