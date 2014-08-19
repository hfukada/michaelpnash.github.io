---
title: Shortcuts for Scala Development in Emacs
author: mnash
layout: post
permalink: /shortcuts-for-scala-development-in-emacs/
related_exlink_5_desc:
  - 
related_exlink_5:
  - 
related_exlink_4_desc:
  - 
related_exlink_4:
  - 
related_exlink_3_desc:
  - 
related_exlink_3:
  - 
related_exlink_2_desc:
  - 
related_exlink_2:
  - 
related_exlink_1:
  - 
related_exlink_1_desc:
  - 
categories:
  - Emacs
  - Scala
---
In the last couple of months I&#8217;ve had a chance to dust off my Lisp-fu (such as it was) again a little, and I&#8217;ve been having fun with Emacs and it&#8217;s Lisp extension language. I&#8217;m using Emacs for Scala development, having gotten tired of the endless upgrade cycles and bugs and performance issues with IDEs.

I do appreciate some of the things IDEs bring to the table, though, and there are still a few things that Emacs just doesn&#8217;t have at the moment. On the balance, though, the sheer speed and power of a dedicated editor like Emacs or Vi is simply superior. I also find I write slightly different, and I think better, code when I&#8217;m doing it with an editor, as opposed to when an IDE keeps &#8220;helping&#8221; me, but that&#8217;s a post for another day.

In my quest to get Emacs customized just right for my Scala development, I find I miss one feature of IntelliJ more than most of the rest: the ability to do a Command-o (Super-o in Emacs-speak) and go directly to a class definition in my project, or Shift-Super-o and go to a file.

In InteliiJ you can also shortcut by typing just the capital letter of a camel-cased class or filename, e.g. SomeBigClassOrOther can be abbreviated SBCOO, instead of the whole thing.

I haven&#8217;t tried that second bit, although I&#8217;m convinced it&#8217;s straightforward as well, but here&#8217;s my first crack at a quick &#8220;find file&#8221; and &#8220;find class&#8221; in elisp, along with the keybindings for them:

I hope someone else finds this useful (or even extends them, and shares!)

Happy editing!

<pre class="prettyprint linenumstrigger linenums">&lt;code class="language-lisp"&gt;
(global-set-key (kbd "s-N") &#039;my-find-name)
(global-set-key (kbd "s-n") &#039;my-find-class)
(setq project-dir (getenv "PWD"))
(defun my-find-name ()
"Find-name-dired in current directory"
(interactive)
(find-name-dired project-dir (format "%s%s" (read-from-minibuffer "Scala File:") ".scala")))
(defun my-find-class ()
"Find-name-grep in current directory for class trait or object"
(interactive)
(setq name (read-from-minibuffer "Object/Trait/Class:"))
(find-grep-dired project-dir (format "class %s" name))
)
(global-set-key (kbd "s-N") &#039;my-find-name)(global-set-key (kbd "s-n") &#039;my-find-class)
(setq project-dir (getenv "PWD"))
(defun my-find-name ()&Acirc;&nbsp; "Find-name-dired in current directory"&Acirc;&nbsp; (interactive)&Acirc;&nbsp; (find-name-dired project-dir (format "%s%s" (read-from-minibuffer "Scala File:") ".scala")))
(defun my-find-class ()&Acirc;&nbsp; "Find-name-grep in current directory for class trait or object"&Acirc;&nbsp; (interactive)&Acirc;&nbsp; (setq name (read-from-minibuffer "Object/Trait/Class:"))&Acirc;&nbsp; (find-grep-dired project-dir (format "class %s" name))&Acirc;&nbsp; )
&lt;/code&gt;
</pre>

[advanced_iframe securitykey="da39a3ee5e6b4b0d3255bfef95601890afd80709" src="http://www.surveymonkey.com/s/H2NJ6MT"]

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