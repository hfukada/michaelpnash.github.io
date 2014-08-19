---
title: 'Emacs Power for Scala Development: Setting Up'
author: mnash
excerpt: Emacs Power for Scala Development, this posting and video looks at getting started, setting up Scala, Emacs, Ensime and related tools, and opening your first project
layout: post
permalink: /emacs-power-for-scala-development-setting-up/
categories:
  - Emacs
  - Scala
---
In followup to my post <a href="http://jglobal.com/emacs-power-for-scala-development/" target="_new">Introducing Emacs Power for Scala Development</a>, here&#8217;s how to set up a new project and get started.

First, some words about assumptions: I&#8217;m doing these steps on my OSX machine that already has Scala 2.10 installed. You can get that from the <a href="http://www.scala-lang.org/" target="_new">Scala-lang website</a>.

You&#8217;ll also need git (command-line version), which you can get from <a href="http://git-scm.com/" target="_new">the git site itself</a>, if you don&#8217;t have it installed already.

I&#8217;m running OSX, with 32GB of RAM on a MacPro, but I use this same setup on my Macbook Air, it doesn&#8217;t take hardly any horsepower at all.

## Getting Emacs

First, you&#8217;ll need Emacs itself. You want at least version 24.2 or later, or most of this won&#8217;t work. The version that comes from <a href="http://emacsformacosx.com/" target="_new">http://emacsformacosx.com/</a> is probably best. Aquamacs doesn&#8217;t work.

Download the .dmg from the above site and install as default, nothing fancy. If you&#8217;re running *nix, get the version appropriate for your distro. If you&#8217;re running Windows, I can&#8217;t help you, despite your great need.

## Getting Emacs-for-Scala

In a plug for my own Github project, you&#8217;ll next need emacs-for-scala installed. This is basically my .emacs.d directory, along with a nice cheatsheet for remembering key bindings, and a bunch of add-ons I&#8217;ve found useful for Scala development.

Installing is pretty straightforward. Just pull from https://github.com/michaelpnash/emacs-for-scala.git into a handy directory, then copy the entirety of the .emacs.d directory from there into your home directory. If you already have an .emacs.d, you might want to back it up first &#8211; don&#8217;t try merging this one over the top of it, it won&#8217;t be pretty.

## Getting a Project from Github (matrix-decider)

Now you need a Scala project to work with.

Falling back on shameless self-promotion, I&#8217;ll again suggest one of mine, Matrix-Decider. You can get it by cloning from here: https://github.com/michaelpnash/matrix-decider.git

If you want to learn more about it, I recommend the links below this article, but any Scala project will do for our purposes here.

Again, use any handy directory, it shouldn&#8217;t matter.

## Generate an Ensime project file

At this point you can follow along with the attached video: It shows how to generate an Emsime project file, then how to fire up Emacs and point Ensime at the proper project. Then it describes how to open dirtree to easily and quickly navigate your project files, and how to open and access your scala files, and what you should see when building.

I suggest you open the video in full screen mode, and make sure you select HD 720 mode so you can see the text clearly.

In later videos we&#8217;ll see how to navigate easily between classes and objects and files in your Scala project.

Don&#8217;t forget all the key-bindings <a href="http://jglobal.com/emacs-for-scala-keybindings/" target="_new">are documented right here</a> for easy reference.



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