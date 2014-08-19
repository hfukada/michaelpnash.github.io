---
title: Matrix Method of Decision Analysis
author: mnash
excerpt: The matrix method can help take subjective opinions and turn them into objective criteria when choosing among several competing alternatives.
layout: post
permalink: /matrix-method-of-decision-analysis/
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
A long time ago, a colleague described to me a method for making decisions in a rational and logical manner. Certain classes of decisions seem to fit this method very well, and the method is, perhaps, just a formalization of something we do naturally when making certain kinds of decisions.

The type of decision this method fits best is where a number of different alternatives must be chosen from, and where there are a set of measurable criteria that can be applied to each choice.

For example: Let&#8217;s say you want to buy a car, and you are faced with a number of possible cars you could buy. You might be able to narrow the decision (that is, reduce the number of choices) by eliminating cars that are unsuitable (e.g. you want a family car, and sports cars do not fit that criteria), or by price (you can afford only $25,000 for a car at most), and so forth. You might still be left with a number of &#8220;finalists&#8221;, let&#8217;s say 3 cars, amongst which you must select one.

This method fits that kind of decision quite well.

I&#8217;m quite sure there&#8217;s a proper name for this method, but I don&#8217;t know what it is, so I call it the &#8220;Matrix Method&#8221; of decision analysis, as that&#8217;s what it involves, a matrix.

Without further preamble, let me describe the method, again using our &#8220;Car&#8221; example. Let&#8217;s say I&#8217;m left with my three cars to choose from, the GM Whatsit, the Ford Flameout, and the Hyundai Horsey. These are the alternatives, which we can list like so, in no particular order:

| Choice         |
| -------------- |
| GM Whatsit     |
| Ford Flameout  |
| Hyundai Horsey |

Now we enumerate a list of &#8220;criteria&#8221;, that is, attributes of the three choices that they share in common, but that have different values (potentially) for each choice. For example, if you want to save money, then price might be an alternative. Each car has a price, so it&#8217;s one of our criteria. We list this criteria and a few others, for example:

| Criteria       |
| -------------- |
| Price          |
| Safety Rating  |
| Interior Space |
| Power Steering |
| Fuel Economy   |

Typically, a decision of this nature involves more than these few criteria, and the method works well for a large number of criteria (in fact, that&#8217;s one place it works best).

Now we have our criteria, we have to rate the relative importance of the criteria amongst themselves. We can use any arbitrary scale, but for our example, let&#8217;s say 1 through 5, where 1 is least important, and 5 is most important. We now assign a value from this scale to each criteria. If two criteria are equally important in our view, they get the same value &#8211; for instance, if price is a 4, and fuel economy is equally important, it also gets a 4. If the safety rating is more important than price, but only a little, it might get a 5. If power steering is a nice to have, but much less important to us than price, it might get only a 2.

We come up with a set of relatively weighted criteria like so:

| Criteria       | Importance |
| -------------- | ---------- |
| Price          | 4          |
| Safety Rating  | 5          |
| Interior Space | 3          |
| Power Steering | 2          |
| Fuel Economy   | 4          |

The values in our scale do matter: we&#8217;re saying here, for example, that price is exactly twice as important as power steering to us. If you need finer gradations, a wider scale helps &#8211; e.g. use 1 to 10, or 1 to 100.

For a criteria to be a good one, there must be a known value for that criteria for each choice &#8211; e.g. we need to know a value for &#8220;price&#8221; (for instance) for every car, otherwise the method can&#8217;t work properly on that criteria.

In the case of power steering, our value for each car might be either 0 (it does not have it) or 1 (it does), unless there are various qualities we&#8217;re taking into account (e.g. this car has power steering, but it&#8217;s terrible, in which case we might need a value from 1 to 3 or some such.

In the case of numeric absolutes, such as fuel economy, we can use the actual value (e.g. 28 MPG, 14 MPG, etc), but we may choose to rank the value on an arbitrary scale instead of the original value &#8211; e.g. something like

| Value     | Score |
| --------- | ----- |
| 10-15 MPG | 1     |
| 16-20 MPG | 2     |
| 20+ MPG   | 3     |

For example.

Once we have a scale for each of our criteria, we determine the value for each criteria for each choice. Here&#8217;s the &#8220;matrix&#8221; part starting:

</table> 
Once we have a value for every choice for every criteria, we&#8217;ll have a matrix like so:

| Choice         | Price | Safety Rating | Interior Space | Power Steering | Fuel Economy |
| -------------- | ----- | ------------- | -------------- | -------------- | ------------ |
| GM Whatsit     | 3     | 5             | 3              | 4              | 1            |
| Ford Flameout  | 2     | 4             | 5              | 4              | 3            |
| Hyundai Horsey | 1     | 5             | 2              | 1              | 5            |

Note that the relative importance of each criteria is not used yet &#8211; now we apply it as follows: For each criteria, we multiply the relative importance of that criteria by it&#8217;s value for each choice, creating a score per criteria for each choice.

| Choice         | Price (4)  | Safety Rating (4) | Interior Space (3) | Power Steering (2) | Fuel Economy (4) |
| -------------- | ---------- | ----------------- | ------------------ | ------------------ | ---------------- |
| GM Whatsit     | 3 * 4 = 12 | 5 * 4 = 20        | 3 * 3 = 9          | 4 * 2 = 8          | 1 * 4 = 4        |
| Ford Flameout  | 2 * 4 = 8  | 4 * 4 = 16        | 5 * 3 = 15         | 4 * 2 = 8          | 3 * 4 = 12       |
| Hyundai Horsey | 1 * 4 = 4  | 5 * 4 = 20        | 2 * 3 = 6          | 1 * 2 = 2          | 5 * 4 = 20       |

Now we add across the matrix, adding up the total weighted values for each option into a single score value per option.

| Choice         | Price | Safety Rating | Interior Space | Power Steering | Fuel Economy | Total Score |
| -------------- | ----- | ------------- | -------------- | -------------- | ------------ | ----------- |
| GM Whatsit     | 12    | 20            | 9              | 8              | 4            | **53**      |
| Ford Flameout  | 8     | 16            | 15             | 8              | 12           | **59**      |
| Hyundai Horsey | 4     | 20            | 6              | 2              | 20           | **52**      |

Now we can sort our options by their total weighted scores. The option with the highest score is, objectively and according to the values we assigned, our best choice.

So the Ford Flameout is clearly the car for me &#8211; but how clearly?

If we want to compare the choices by percentage, we can compute the perfect score, e.g. a hypothetical car that had a perfect rating for every criteria, which in this case would have resulted in a score of 85, then compare each of our choices scores to that:

| Choice         | Weighted Score | % of Perfect Score |
| -------------- | -------------- | ------------------ |
| GM Whatsit     | 53             | 62.3               |
| Ford Flameout  | 59             | 69.4               |
| Hyundai Horsey | 52             | 61.1               |

So although my Flameout won, it was only by a few percentage points in reality, not a landslide, and the Horsey and the Whatsit were neck-in-neck. Overall, no car really scored that high in absolute terms, so perhaps my correct choice isn&#8217;t even in the table.

Often this answer will surprise us, but the matrix tells us exactly \*why\* its the best, so if we&#8217;ve scored a choice incorrectly, or if we want to go back and re-evaluate our weighting of criteria, we can.

I am often surprised by how often my intuitive choice is not the same as the one the matrix gives me, while at the same time when I go back and confirm that my importance ratings were actually correct, I see that the math actually leads me to a rationally correct choice every time.

It&#8217;s an objective way to make a decision, or at least understand a decision.

This is a very simple method, and of course any spreadsheet can be used to work out the numbers and do &#8220;what ifs&#8221; on the results.

I hope it&#8217;s valuable to someone else out there &#8211; I&#8217;ll let you decide <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Matrix Method of Decision Analysis" class="wp-smiley" title="Matrix Method of Decision Analysis" /> 

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