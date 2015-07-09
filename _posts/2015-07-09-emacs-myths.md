---
title: Emacs Myths
author: mnash
excerpt: Misconceptions about the worlds most powerful editor
layout: post
permalink: /emacs-myths/
categories:
  - emacs
---
  
Something I encounter a lot in my travels is surprise from many of my colleages that I use a thirty-year old editor application, instead of a so-called 'modern' IDE.

It actually took me a long time to make the switch, and I will still break out an IDE or other tool from time-to-time, but I'm very happy with my choice.

I won't explain my reasoning here, that's the topic for another article. What I will say is that a number of myths and misconceptions prevented me from making the switch for a very long time. Now that I use Emacs regularly, I hear these same myths and misconceptions repeated a lot by my colleagues, and I worry that they may be missing out on a great tool as a result.

# Escape-Meta-Alt-Control-Shift
Many humorous names exist for Emacs (Emacs Makes All Computers Slow is another one), but the Escape-Meta-Alt-Control-Shift one I think is emblematic of the greatest Emacs myth of all: that you need to learn all sorts of hand-twisting keyboard shortcuts in order to learn Emacs.

What's interesting is that this is not just an exaggeration - even Emacs users like to make fun of some of the more bizzaire shortcuts we work with - it's actually entirely false.

I'm using Emacs write now to write this article, and I am quite able to do so without using any keyboard shortcuts at all. I have a menu at the top of my screen that shows all the major commands, like like any other editor. I can use the arrow keys to move around if I want to, or click on and select text in a gui-like manner all I want.

I can drag and resize blocks of text - I can show a window that tells me how far into the file I am in a visual manner (like Sublime Text's feature), all without any special key gymnastics.

I can even use a right-click context menu straight from the -gasp- mouse!

Emacs does not at all require special key combos to be learned, or to use. They are handy, once you get good, of course, simply for efficiency and speed. I can hit a key combo many times faster than I can even get my hand over to my mouse, much less click a menu.

But I don't *need* them.

# Emacs for Terminals
Emacs *can* be used in a text-only mode, much like Vim can. I occasionally use it that way if I'm ssh-ed in to a remote box, and it's handy, because all my editor commands and such work the same way.

It is not, however, how I normally use Emacs. I'm using Emacs right now in a local mode, with full GUI support, windows, panes and panels, the works.

# Emacs is Hard to Learn
My first reaction when I hear this is to say "so?". Anything that saves me many minutes (at least) per day is, to my mind, worth some effort to learn. However, when I dig a bit deeper, I find this is also patently false.

Emacs is in fact very easy to learn. You can get started in Emacs in *minutes*, at most.

What can take a long time is to *master* Emacs, but that's something different. It's a deep editor, with thousands of plugins, infinitely configurable. Mastering it can take years, but that doesn't mean it's hard to get started - it's not.

Heck, Emacs has it's own tutorial built into it, for that matter, not to mention hundreds of sites, videos, books and courses, both for the beginner and the adept.

Interestingly, a lot of people find that they already know a bit of Emacs, even though they've never actually used it. That's because the keyboard shortcuts in Emacs are so popular that they find their way into other products: Google Docs, for instance, can use Control-N to go to the next line, Control-P to the previous, Control-A for start-of-line, Control-E for end, and so forth (in addition to arrow keys and mouse movements, of course).

These are all Emacs shortcut keys, so if you've been doing these keys in Gdocs, you already know some Emacs.

# Emacs is Less Powerful and an IDE
This one depends a bit on your definition of 'powerful'. I use Emacs for developing Scala code, among other languages, and I don't know of an IDE that can work with *all* the languages I work with that is anything like as powerful as Emacs.

I do, however, use custom plugins for different language: I use Ensime, for instance, for Scala, and I have custom modes for Erlang, Elixir, Haskell, Lisp, Clojure, and many others.

A big draw for me with Emacs is that I use the same editor for all of these, and can switch from one language to another with no jarring cognitive changing of gears to swap out one IDE for another.

# Emacs can't use Proportional Fonts
Also mythical - and probably a hold-over from when Emacs was terminal-only (which hasn't been the case in a long time).

You can use just about any font you want in Emacs, proportional or otherwise. I'm font of the Source Code Pro font myself, but I change it up from time to time. Switching is trivial, basically.

# Emacs can't be Graphical
Also false: I actually use Emacs to browse directories of images, and can open an image directly in an Emacs window commonly.

I think this one stems from Emacs' origins as a terminal-mode editor, but it's evolved, I assure you.

I hope dispelling some of these long-standing myths might encourage a few more developers to have a look at Emacs. It's not for everybody, but it might be for *you*.

