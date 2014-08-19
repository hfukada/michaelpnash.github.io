---
title: A Month with Emacs
author: mnash
layout: post
permalink: /a-month-with-emacs/
categories:
  - Emacs
  - Scala
---
I code for a living &#8211; well, sometimes I help other people code, but I spend a pretty fair amount of time touching code myself. That&#8217;s the way I like it, and I hope to do it for a long time to come.

Given that I&#8217;ve been doing it for a long while already, finding ways to do it well that are sustainable makes sense to me.

As a result, I&#8217;ve re-acquainted myself with Emacs, in a big way. As I went, I developed a <a href="http://jglobal.com/emacs/" target="_new">video series to document using Emacs for Scala development</a>.

Someone once described building your emacs config (feels inadequate to call a few thousand lines of Lisp a &#8220;config&#8221;, but still) as the equivalent of a Jedi building his own light-sabre. Only after you&#8217;ve done it are you a true Emacs user.

Well, I&#8217;ve got my light-sabre pretty much where I want it, and I&#8217;ve been doing all my Scala development for at least the last month exclusively in Emacs. There are still plenty of tweaks I&#8217;d like to make, but they&#8217;re small fry compared to what I&#8217;ve got working already.

I thought I&#8217;d report on progress, in case it&#8217;s useful for other people planning the adventure.

### Another 9 years, 11 months&#8230;

First off, I&#8217;m hardly &#8220;done&#8221; learning Emacs, whatever that means. I&#8217;ve known the basics of Emacs for many years, having used it off and on for decades, along with many other editors, even VI. Yes, I&#8217;m bi-editorial, or whatever the correct term is: I can use (and appreciate) both VI **and** Emacs. (This may get me burned at the stake by both religions, I&#8217;m not sure).

In any case, Emacs is not my first rodeo, not by a long shot. I&#8217;ve used IntelliJ, Eclipse, IBM&#8217;s VisualWorks, JEdit, Sublime Text, TextMate, and dozens more. Hell, I&#8217;ve even used &#8220;ed&#8221;, in case anyone&#8217;s left that knows what that is besides me <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile A Month with Emacs" class="wp-smiley" title="A Month with Emacs" /> 

### Ergonmics

After trying just about every kind of keyboard there is, I settled some time ago on an IBM Model M. When I can&#8217;t get a new one, I use the Unicomp version. If I must, I use a trackball, or an Apple magic trackpad. I do have a couple of mice as well, but find when I need a mouse I actually need a trackpad.

Emacs, plus a few tricks like Spectacle and Quicksilver, allow me to hardly ever touch that trackpad/trackball, and this is my win ergonomics-wise. It&#8217;s quite a bit, it turns out. Emacs, quite famously, uses a number of combination keys (it&#8217;s sometimes called Escape Meta Alt Control Shift, in fact), but these can be remapped however you want, and it&#8217;s still far better than taking your hands off the home row.

For my home-office setup, I actually have a few more gadgets to make things even more efficient, but that&#8217;s another later post.

### Speed

While I&#8217;m still learning, I can now safely say that I can edit faster with Emacs that I can with VI. That&#8217;s pretty fast, as VI is no slacker. There&#8217;s still a few keybindings I&#8217;d like to tweak, sometimes I miss things like &#8220;change word&#8221; (yes, I know there&#8217;s a way to do that in Emacs). It&#8217;s like typing Dvorak &#8211; at first you&#8217;re stumbling around mostly breaking stuff, then it&#8217;s not bad, then it&#8217;s better&#8230;

I&#8217;m at the point now where every now and then I get into the flow pretty well, and I stop thinking about the editor entirely, and I&#8217;m just thinking code. For those brief moments, which are slowly getting longer, I&#8217;m smoking along pretty good, cranking out and working on Scala code far faster than I can do it in IntelliJ, which is also pretty fast. I&#8217;m also writing a book in Emacs &#8211; which means I&#8217;m using the same editor to write a book as to write my code, another big plus.

More than just fast, I find Emacs **efficient**. That is, you don&#8217;t do a lot of messing with the editor to get work done &#8211; it doesn&#8217;t get in the way, or change the way you want to work. I can have an editor up and running, showing me the code in a project, in about two seconds on a feeble laptop. I can use the same editor for any language I choose, and for any kind of file I want to edit, even over an SSH link to a remote box. I can (and have) use an iPad with a bluetooth keyboard with a remote AWS instance as a development box, all with the same editor.

### What do I miss?

I miss the clever feature in IntelliJ that will highlight unused imports. I miss code completion of the .apply method on case classes. I miss the ability to browse external dependencies easily. That&#8217;s about it. I can fix all of these, in time.

I don&#8217;t miss the crashes, I don&#8217;t miss when the IDE craps out and disappears, I don&#8217;t miss the slowdowns and painful delays starting up. I don&#8217;t miss upgrading the plugins every seven minutes, I don&#8217;t miss the random bugs, I don&#8217;t miss my IDE scrambling my refactors to the point where I revert from source control on a regular basis.

GUI-based IDEs can be prettier, but I&#8217;m not coding for pretty, I&#8217;m coding to get work done, and Emacs is substantially easier to read the code, find the code, edit the code &#8212; and that&#8217;s the job I want my editor to do.

### Multi-Lingual

Of course, I don&#8217;t *only* do Scala, I actually work in a number of languages from time to time, although Scala is my go-to stack. Emacs comes with me: everything works if I&#8217;m cranking out Haskell, Clojure, whatever. That&#8217;s pretty nice, even though it doesn&#8217;t directly help me with my Scala development. Of course, even writing Scala I still have to write Javascript (or Coffeescript), HTML, Markdown&#8230; so in that sense, it&#8217;s great to do all of these in the same powerful editor.

### Conclusion

I&#8217;m sold. I won&#8217;t be removing all other IDEs, as once in a while they do something extra I really want, and it&#8217;s important to keep your familiarity with other IDEs, as your teammates might be using them, and you don&#8217;t want them to be forced to use something they don&#8217;t know.

But my go-to editing suite is now my custom Emacs setup.

What&#8217;s your IDE/Editor of choice? [Take Our Survey][1] and let us know!

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

 [1]: http://www.surveymonkey.com/s/Z5G5FVR