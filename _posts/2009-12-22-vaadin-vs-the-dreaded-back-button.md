---
title: Vaadin vs. the Dreaded Back Button
author: mnash
layout: post
permalink: /vaadin-vs-the-dreaded-back-button/
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
---
I owe the <a href="vaadin.com" target="_new">Vaadin</a> framework an apology. When demoing some research I&#8217;ve been doing on Vaadin to a colleague today, he asked if Vaadin, like many Ajax-oriented frameworks, &#8220;breaks&#8221; the browser&#8217;s back button. What he meant was that when you&#8217;re working in a Vaadin app, pressing your normal &#8220;back&#8221; button in the browser takes you to whatever site you were visiting before you came to the Vaadin app, not to the last place you were **inside** the Vaadin app.

I told him yes &#8211; and hence the source of my apology. Strictly speaking, I was correct: if you take no extra care, then clicking the browser &#8220;back&#8221; will take you out of your Vaadin app altogether. However, this bothered me, and I went home to tinker with it a bit. 

It turns out that Vaadin has full and easy support for &#8220;back&#8221;, bookmarking, and all of the other URL goodness you might expect in any other kind of web application or site, and it&#8217;s so easy. 

By adding a component called a UriFragmentUtility to your first Vaadin window, you get a &#8220;hook&#8221; into the URL of your application, with the ability to both read and write the &#8220;fragment&#8221; portion of the URL, that is, anything after a # sign in the URL. For example, if your application&#8217;s URL is www.foo.com/myapp, then www.foo.com/myapp/#bar will have a &#8220;fragment&#8221; of &#8220;bar&#8221;. 

I had already wired up my Vaadin to use Spring to dependency-inject it&#8217;s components, so I was able to map this fragment directly to the Spring ID&#8217;s of my components. So when my app says &#8220;www.foo.com/myapp/#bar&#8221;, I can have it automagically find the component &#8220;bar&#8221; and display it in the main area. Invalid names (if the user types a URL I don&#8217;t understand) can easily be handled with an appropriate message, or I can just send them back to the main menu.

The reverse is also true: if the user selects a new item from my menu, and the application loads the component, I can use the UriFragmentUtility to set the fragment seen in the URL box &#8211; so the user clicks a menu choice, and the URL changes to &#8220;www.foo.com/myapp/#baz&#8221;.

This means bookmarks work as well: if I bookmark &#8220;www.foo.com/myapp/#baz&#8221;, and come back tomorrow, it will work just as expected, taking me directly to the &#8220;baz&#8221; &#8220;page&#8221; of my app (I use &#8220;page&#8221; cautiously, as there is in fact no such concept as a &#8220;page&#8221; in a Vaadin app).

It&#8217;s equally easy to handle URL parameters, or to read a format of URL that doesn&#8217;t include the &#8220;#&#8221;, if you are bothered by it. So I can do things like &#8220;www.foo.com/myapp/someplace/1234&#8243;, and automatically load the component &#8220;someplace&#8221; and pass it the parameter 1234, or &#8220;www.foo.com/myapp/someplace?id=1234&#8243; if you prefer.

All easy, all friendly to the browser back-button &#8211; which now does exactly what the user would expect &#8211; takes him/her to the last place in the Vaadin app he was.

So as far as I&#8217;m concerned, Vaadin **doesn&#8217;t** break the back button at all, and leverages it, bookmarking, and URLs and general very easily.

This also solves the issue of how to Search-Engine Optimize a Vaadin app &#8211; but that&#8217;s another post for a later day.

Thought I&#8217;d pass that along.