---
title: 3D Rendering on AWS
author: mnash
layout: post
permalink: /3d-rendering-aws/
categories:
  - Tools
tags:
  - 3D
  - AWS
  - Blender
  - Rendering
---
Yesterday I had an opportunity to conduct a bit of an experiment: I wanted to see if 3D rendering, specifically rendering model frames from a Blender model, could be done efficiently and quickly on cloud virtual servers. I know there are many render farms that do exactly this, but of course in the case of someone else&#8217;s render farm you&#8217;re never quite in full control of the process, or of the cost.

In any case, I wanted to try it out with various configurations of AWS (Amazon Web Services) virtual machines, and learned a lot &#8211; so I&#8217;d like to share the outcomes in case they&#8217;re valuable for others trying the same things.

I began with a AWS instance of type c3.large, which is a 64-bit VM with 7 ECU (Elastic Compute Units) roughly equivuilant of 2 cores, 1.7 GB of RAM, and moderate network performance. 

Then, to make a consistent timing run, I selected a well-known model, the BMW model discussed [here][1].

I fired up my instance, downloaded a copy of Blender 2.69 and built a quick script like so:

<pre>./blender -b $1 -t 0 -s 1 -e 1 -a -x 1 -o //render
</pre>

This script, in a nutshell, says &#8220;run blender from the current dir, using the model passed as the parameter to this script, and render the first frame (from frame 1 to frame 1).

On the initial box, this took 2 minutes, 55 seconds.

By way of comparison, my old Mac Pro (2.66 Quad-core Xeon, 12GB 1066MBz DDR3 RAM) took 3 minutes and 3 seconds, so not too shabby.

Then we started tinkering: After some reading on the AWS site and elsewhere, we thought to try a high-GPU AWS instance, and direct Blender to use the GPU.

There were a few false starts at this point: Amazon correctly points out that there&#8217;s no point in having the instance set up with a GPU without using the proper drivers, and we picked the wrong machine image (AMI, Amazon Machine Image) the first time around: The NVIDIA GRID one didn&#8217;t help us, and is based on Fedora, apparently. Once we came back from that rabbit-hole, we tried an Ubuntu GPU image on a g2.2xlarge instance, which is a 26 ECU machine with 15 GB of RAM and high network performance.

We used a slightly modified version of our script:

<pre>/blender --python gpu.py -b $1 -t 0 -s 1 -e 1 -a -x 1 -o //render
</pre>

With the gpu.py containing the code:

<pre>import bpy

bpy.context.user_preferences.system.compute_device = &#039;GPU&#039;
</pre>

To select GPU computation, instead of only relying on the CPU.

This brought our compute time for a single frame down to 32 seconds <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile 3D Rendering on AWS" class="wp-smiley" title="3D Rendering on AWS" /> 

That&#8217;s roughly 20% of the original 2:55 time, and certainly puts my local machine to shame.

Of course, doing multiple frames with higher cycles means the overall time to compute goes back up &#8211; just as it would also go back up on a local system, but with the AWS setup, we can ship a frame or a few frames to separate machines, have them all process in parallel, and put the result back together with an actual elapsed time not much more than doing a single frame at the best resolution (assuming you have one machine per frame &#8211; which of course is a lot of machines &#8211; but Amazon have a \*lot\* of machines).

We have several other experiments to run, but wanted to share the results so far &#8211; we&#8217;ll post more when we discover it, and very much welcome input into our experiments!

Many thanks to **ideasman42** on IRC for a few key tips that kept us going when we were close to stuck on setting Blender options!

 [1]: http://blenderartists.org/forum/showthread.php?239480-2-6x-Cycles-render-benchmark