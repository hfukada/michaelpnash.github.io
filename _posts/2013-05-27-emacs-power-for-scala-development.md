---
title: 'Emacs Power for Scala Development: Introduction'
author: mnash
excerpt: "Your tools make a difference. By assembling a powerful set of tools you can make your Scala development quick and efficient, and get many other jobs done faster too. Emacs and Scala are a great fit together, in this post we'll explain how I've assembled a combination of tools for fast Scala work."
layout: post
permalink: /emacs-power-for-scala-development/
categories:
  - Emacs
  - Scala
tags:
  - Emacs
  - Scala
---
I&#8217;ve blogged before about using <a href="http://www.gnu.org/software/emacs/" target="_new">Emacs</a> for <a href="scala-lang.org" target="_new">Scala</a>, but I&#8217;ve recently upgraded my Emacs-fu a bit further, and wanted to share the latest state of all the power of Emacs available for Scala development (along with a few loosely related power tools).

Emacs is an entirely incredible editor. I&#8217;ve had a long and sometimes fairly distant relationship with Emacs over the years.

For a long time I was strictly a Vim guy, finding in it&#8217;s conciseness and simplicity all the power I needed. It&#8217;s still my goto tool for a quick-and-dirty edit, and is, I know, capable of much more than I do with it.

I had used Emacs, but found it too much for me in most cases. I still pulled it out once in a while, but it wasn&#8217;t until I started doing more Lisp work (and a bit of Prolog) that I really got it. Emacs isn&#8217;t just an editor at all &#8212; it&#8217;s practically an operating system, with it&#8217;s own programming language (eLisp) to boot!

It&#8217;s great power comes from two things, in my view: one is that it&#8217;s a keyboard editor, e.g. you can do everything emacs does entirely with the keyboard, no mouse required.

I&#8217;m no mouse luddite (actually, I prefer trackpads and trackballs), but I do fully recognize that for sheer editing efficiency, there&#8217;s nothing so fast as they keyboard, especially if you&#8217;re using &#8220;normal&#8221; keys (e.g. the typewriter set, not a bunch of extra F-keys that might not be on all keyboards). The difference is not small, it&#8217;s huge. You can literally work many times faster with just the keyboard &#8212; this is covered extensively elsewhere on the web, have a look around.

I&#8217;ve also blogged about why I prefer Scala as my go-to language, so I&#8217;ll just refer you to my other posts if you&#8217;re interested. Suffice it to say I&#8217;ve tried quite a few languages, and Scala blows the doors off the lot of them for just plain practicality.

So, how do we put the power of Emacs with the practicality of Scala?

You can start with nothing, actually. Straight Emacs, right out of the box, makes an awesome Scala editor, as Scala files are just plain text after all, and plain text is Emacs&#8217; middle name.

You can take it much further, however, starting with Scala Mode, which gives you basic syntax highlighting, making it a bit faster and easier to read your Scala source.

Beyond that are tools to help navigate and refactor. My favorite of these is Ensime, as I&#8217;ve discussed before.

The latest version (I&#8217;m using 0.9.8.9 with Scala 2.10) is getting pretty darn good. By this I mean it&#8217;s giving my other go-to tool for Scala development, <a href="http://www.jetbrains.com/idea/" target="_new">Jetbrains&#8217; IntelliJ IDEA</a>, a run for it&#8217;s money.

Not in the &#8221;pretty&#8221; department &#8211; that&#8217;s not what Emacs does. Just in the plain capability mode. It was always miles ahead in terms of speed &#8212; the latest version 13 early-access of IntelliJ is much better speed-wise than it used to be, but Emacs still runs circles around it. The reason is simple: Emacs is trying to do far less than IntelliJ is &#8212; it&#8217;s not an IDE, per se, just an editor.

Even running Ensime, though, which gives it most of the support of a true Scala IDE, it&#8217;s still much faster in just sheer editing, and about the same on doing various refactors, finding imports, and so forth.

It&#8217;s been said that Emacs is like a light-saber. You don&#8217;t just go to the store and buy one, you build your own. I&#8217;ve been doing just that, refining my Emacs configuration to do exactly what I want. It&#8217;s almost unfair to call what Emacs does &#8220;configuration&#8221;, though &#8212; it&#8217;s much more. I have a series of a dozen or so entire packages of elisp code in my .emacs.d directory (<a href="http://github.com/michaelpnash/emacs-for-scala" target="_new">it&#8217;s all on github, right here</a>, if you want to have a look).

This not only set up my emacs with Ensime, Scala mode, and all the goodness I need for banging out Scala fast and accurate, it also has tools for helping with file navigation, beyond what Ensime does already for navigating Scala source.

My favorite at the moment is dirtree, which gives me a simple tree view of selected directories, and lets me whip through them effortlessly, all with just the keyboard. Sunrise commander is another much more powerful alternative &#8212; I&#8217;ve got both configured, and I jump to Sunrise when I need to really work with directories more than just navigate around quickly. Either of these are worth of their own blog posts, and may well get them in the future.

On the right is a screenshot of Dirtree, with a Scala file (using Ensime and Scala mode) open in the other buffer.

<div id="attachment_1962" style="width: 310px" class="wp-caption aligncenter">
  <a href="/wp-content/uploads/2013/05/dirtree.jpg"><img class="size-medium wp-image-1962" alt="dirtree 300x162 Emacs Power for Scala Development: Introduction" src="http://jglobal.com/wp-content/uploads/2013/05/dirtree-300x162.jpg" width="300" height="162" title="Emacs Power for Scala Development: Introduction" /></a> <p class="wp-caption-text">
    A screenshot of Dirtree in Emacs with Scala Mode and Ensime
  </p>
</div>

You can see at the bottom of the screen that I&#8217;m on the master branch for my git repo, and that Ensime is aware I&#8217;m editing a Scala file. If any lines have an error, I see them immediately. For example, kill an import statement, and the resulting error is highlighted (and the error itself, an unknown type, shown in the minibuffer at the bottom of the screen):

<div id="attachment_1964" style="width: 310px" class="wp-caption aligncenter">
  <a href="/wp-content/uploads/2013/05/witherror.jpg"><img class="size-medium wp-image-1964" alt="witherror 300x162 Emacs Power for Scala Development: Introduction" src="/wp-content/uploads/2013/05/witherror-300x162.jpg" width="300" height="162" title="Emacs Power for Scala Development: Introduction" /></a> <p class="wp-caption-text">
    An error highlighted in Ensime after deleting an import
  </p>
</div>

Then I can hit C-c C-r t (this is easier than it looks, I just hold down Control, hit c, then r, release control, then hit t. It takes way less time to do it than describe it). I get a popup of suggested imports, like so:

&nbsp;

<div id="attachment_1965" style="width: 310px" class="wp-caption aligncenter">
  <a href="/wp-content/uploads/2013/05/importpopup.jpg"><img class="size-medium wp-image-1965" alt="importpopup 300x162 Emacs Power for Scala Development: Introduction" src="/wp-content/uploads/2013/05/importpopup-300x162.jpg" width="300" height="162" title="Emacs Power for Scala Development: Introduction" /></a> <p class="wp-caption-text">
    Import popup in Ensime in Emacs for Scala
  </p>
</div>

The first one is the right one, so I just hit enter, but there&#8217;s myriad ways to navigate to the right one if it&#8217;s not the top of the list. When I hit enter, my import is back, and my error goes away. It&#8217;s very, very fast.

One thing IntelliJ had was the ability to quickly and easily move around lines or blocks of Scala code, so I added move-text, a package that I&#8217;ve bound to Meta-Up, Meta-Down, allowing the same quick and easy re-organization of lines of code without having to cut and paste.

For git access, I can drop to the command-line of course, and often do (I use Zsh, which has excellent integrated git command-line tool support), or I can do that from &#8212; you guessed it &#8212; Emacs. I use Magit, which gets me quick and easy access to git right from within Emacs.

If i need to track my time (if I&#8217;m developing for a client, for example), I can stay right in Emacs and use the amazing <a href="http://orgmode.org/" target="_new">Org-mode</a>, from organizing the tasks in my project, though tracking my time, all the way up to preparing my time report for billing.

One of the benefits of doing everything in Emacs is that I can use a common set of keybindings (which determine what keys do what in the various Emacs modes). This means once my fingers learn what they&#8217;re doing, I stop thinking about keyboard shortcuts and just burn out the work. It becomes unconscious after a while, I don&#8217;t think &#8220;oh, I need to get to the end of the line&#8221;, I&#8217;ve already hit C-e by the time the thought starts to register. My fingers don&#8217;t leave the home row for minutes at a time, and the peck-peck&#8230; mouse&#8230; peck-peck&#8230; mouse drudgery just stops. Emacs is fast enough to not break my flow of coding, so put it all together and I can get more done in an hour than I could have in three with a different toolset.

I&#8217;m working on a series of posts to show all of this in detail, from the setup of your own Emacs through the cloning of a Scala project, through planning a series of edits to the project with Org-mode, and tracking items to do and time spent on them, all the way through refactoring, running tests, pushing changes to github, to generating my time to send a bill, all in &#8220;real-time&#8221;.

In the meantime, here&#8217;s a short video showing me correcting an error in Emacs/Ensime, as I describe above.



<div class="g-plusone" data-annotation="inline" data-width="300">
</div>

<!-- Place this tag after the last +1 button tag. -->

  


<div class="st-callout hastitle lightblue center" >
  <h4 class="st-callout-title ">
    Principles and Practices
  </h4>
  
  <div class="inside">
    <i>Tired of the Software Development Grind?</i> Know it can be done better? Check out my book: <a href="/principles-and-practices">Principles and Practices of Software Craftsmanship</a> or sign up for my <a href="/dispatches/">Craftsmanship Dispatches</a> newsletter.
  </div>
</div>

<div class="clear">
</div>
