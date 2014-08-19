---
title: Emacs Collaborative Editing
author: mnash
layout: post
permalink: /emacs-collaborative-editing/
livefyre_version:
  - 3
categories:
  - Emacs
  - Remote Development
---
Pair programming is generally thought of as something done in close physical proximity, usually with two developers sitting right alongside each other at a single computer, with one mouse and keyboard.

In most cases, when it&#8217;s done right pairing actually allows for higher productivity and lower defect rate than a single programmer working alone, although in a lot of companies there&#8217;s still this stigma of &#8220;waste&#8221; about it. Managers see two programmers working on one problem and think &#8220;why can&#8217;t they each be working on their own problem &#8211; we&#8217;d get twice as much done!&#8221;. This only happens with manager that think that programming has something to do with typing speed, which it really doesn&#8217;t. (Sure, it helps to type fast so that when the ideas some you can get them out of your head and onto the screen quickly, but there&#8217;s a lot more value in the thinking than the typing). Pair programming is the demonstration of the fact that two heads really are better than one.

Recently, though, it&#8217;s become much more common to see remote developers pair with each other, working on the same problem together via some kind of screen sharing facility. This works, and I&#8217;ve done it myself for many years, with varying degrees of success.

As people have observed in many other places on the internet, remote work in general takes a slightly different set of disciplines than co-located work. Once those disciplines are adopted, though, productivity can easily be equal, and I would maintain, greater in many cases, then co-located development.

The tools that can be used for remote pair programming, though, have lagged somewhat behind what&#8217;s available on the desktop directly. Applications such as TeamViewer, Join.me, ScreenHero, GotoMeeting, and others all take the approach of &#8220;sharing&#8221; the screen of one computer, displaying it on both computers. This is helpful, but is limiting in many ways.

When using screen sharing, only one developer can be editing the document at a time: The better apps allow &#8220;control&#8221; to be easily switched back and forth between the two participants, but they are running a single version of the editor or IDE on one or the other of their computers. The participants must synchronize, usually through chat or a VOIP/Audio connection, who has control at any one time, and it&#8217;s not easy for them to split up on a problem then recombine again a few minutes later.

Different screen resolutions are also a problem: if one developer is on a laptop and the other has two large desktop monitors, the desktop user must only use a small area of his screen, or the laptop user must scroll around fiendishly on his little screen.

Also, one participant must set up the IDE or editor and the other must live with that setup: For example, if both people are using IntelliJ IDEA, and one is on a Mac and the other on Windows, the key shortcuts will be different between the two, so when the guy on the mac takes over the screen, he&#8217;s slowed down by pushing all the wrong keys when he goes to do an edit on the IDE running on windows.

A flow that I&#8217;ve found happens in my current team is also tricky with this set up: When pairing, I find that the pairs often work on a collaborative problem for a while, then realize they&#8217;ve got a bit of work that can be done individually, so the &#8220;visitor&#8221; gets up, goes back to his desk, catches up with the code (did the other guy push?) and works for a few minutes. Now he hits a tough spot, where he wants the extra eyes of his pair, so he reverses the procedure, goes back to his partners desk, catches him up on the code&#8230;

Also, we sometimes hit a spot where we want more than two pairs of eyes on it, we&#8217;d like to show the whole team a piece of code and get input. Tricky, no matter how big your monitor is, there&#8217;s only so much physical space around a desk. And forget actual three-way collaboration, it just doesn&#8217;t happen, even if it could.

In my experiments with Emacs I&#8217;d found that I could use it in character-mode, in a terminal program such as iTerm2, in conjunction with tmux, and get some pretty good sharing that way.  One user could start the tmux session, then the second could attach to that session. Either could then fire up Emacs (on the same server), and share the Emacs instance, switching back and forth on editing seamlessly.

Emacs looks a little different in character mode, but is quite usable.

However, I&#8217;ve recently found what I think is an even better way to collaborate in Emacs&#8230;

### Rudel

The <a href="http://rudel.sourceforge.net/" target="_new">Rudel</a> project adds a very handy collaboration mode to Emacs that is very different from screen (or even window) sharing.

In Rudel, one party initiates a *session*, essentially becoming the host of the pairing session. That user can then open buffers and, with a keystroke, *publish* them. The user on the other end then *subscribes* to the document (again, with a quick keystroke). At that point you&#8217;ve got a buffer open that is shared between the users, but shared quite differently than sharing a window such as VNC.

The buffer is open and visible to both partners, and any edits made by one are immediately visible to the other, but each person can scroll to a different point in the buffer, even outside the view of the other party, and continue editing.

There&#8217;s no need for one pair to &#8220;have control&#8221;, as both have full control all the time, and can do whatever they need to to that buffer (or any other buffer). Each person is free to open a shared or non-shared file in their local Emacs, so for example, one of the pair can be working on the test while the other person gets the last test passing, then vice versa. No more watching the other person type (except when that&#8217;s appropriate!).

Each developer can have his own keybindings, as customized as he wants, as he&#8217;s still working on his own local copy of Emacs. One can be in XEmacs, one in Emacs for OSX, and a third using character-mode (-nw) Emacs in a Terminal &#8211; it all works just the same.

I&#8217;m making a couple of minor tweaks to my Emacs config for convenience: For instance, I&#8217;d like to auto-publish each new file as I open them from dirtree mode, and that&#8217;s easy enough &#8212; two lines of eLisp and it&#8217;s working.

I&#8217;ve also added the ability to auto-subscribe, so that when a new document is published, any remote members of the session automatically subscribe to them, making it easier when jumping around between a bunch of files.

The flow using Rudel takes some getting used to, but it solves a great many of the problems of traditional screen-sharing, and of course, being an Emacs extension it is infinitely extensible and customizable, which takes it miles beyond all other screen-sharing solutions right away.

Here&#8217;s a screen-grab of a Rudel collaborative session in progress:

[<img class="aligncenter size-medium wp-image-2367" alt="rudel2 300x259 Emacs Collaborative Editing" src="http://jglobal.com/wp-content/uploads/2013/06/rudel2-300x259.jpg" width="300" height="259" title="Emacs Collaborative Editing" />][1]

At the top of the screen you can see the names of the users in the session, and the color assigned to their edits. As they each make edits, their changes appear in their distinct color, making it easy to keep track of who&#8217;s doing what, even if there are three or more people on the session. The edits appear simultaneously, as they&#8217;re typed, which is a bit odd looking if you&#8217;re not used to collaborative editors, but very cool to see!

In this case we only have one buffer visible, but there&#8217;s nothing to prevent you having a split-screen with several buffers being collaborated on at once (think: class and it&#8217;s unit test, for instance), and each person can work on the section they want on any file.

I&#8217;ll post an update when we have a chance to work with it a bit more, but so far I think there&#8217;s a lot of promise for remote collaboration in Rudel and Emacs!

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

 [1]: http://jglobal.com/wp-content/uploads/2013/06/rudel2.jpg