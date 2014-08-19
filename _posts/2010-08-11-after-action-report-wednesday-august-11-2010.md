---
title: After-Action Report, Wednesday, August 11, 2010
author: mnash
layout: post
permalink: /after-action-report-wednesday-august-11-2010/
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
I am pleased to report that the campaign goes well thus far.

We met the enemy at the border of Weblogic, and battle was joined, SVN commits clashing with intractable lengths of binary spaghetti at every turn.

Our original plan was to crush all remote beans entirely, liberating the entire application from this particular scourge. Much progress has been made towards this goal, although the enemy is powerful and resourceful.

We can confirm that at least five of our opponents fell early in the glorious battle, with minimal losses on our side, despite the heavy resistance. At several points in the battle the WTF/minute meter was rising to dangerous levels. One particularly brave refactor was rolled back in a blaze of glory, still muttering &#8220;stay in target directory&#8230; stay in target directory&#8221;&#8230;

Our initial attempt at penetration of the enemy&#8217;s lines was at the JMX pass. Despite valiant attempts by our brave tests, we were eventually defeated in this attack by proprietary &#8220;extensions&#8221; to what should have been well-accepted standards. The enemy knows no shame, and will stoop to perverting even innocent RMI for it&#8217;s nefarious purposes. In fact, they dredged up what should have been long-forgotten and discarded protocols to throw us off the track, even resorting to JMX over IIOP, with proprietary client libraries, which was too much for us &#8211; we could not withstand that level of firepower. We had to find another way.

We were repelled by the evil machinations of the enemy&#8217;s classpath conflicts at the battle of the EAR, but were able to outflank them and retreat to a previous revision number with minimal losses. We then regouped and attacked again in the region of the remote stateless session bean, and only one of the enemy escaped our wrath. We will be watching this one remaining combatant carefully, and at his first slipup he is sure to be doomed as well. We have assigned our best integration test to watch his every move.

Despite attempts to deceive our troops with obscure and fiendish JNDI naming practices, we were able to ensnare many of the enemy in our powerful web of functional tests, where they can do no further harm.

At least four entire modules of the enemy&#8217;s forces did not survive the encounter!

We have won this conflict for now, yet many challenges still lie ahead in future battles. The enemy used many clever tactics this time, but we have not yet encountered their ultimate weapon: the greatly-feared **container-managed entity bean!** Weapons of mass deprecation of this nature must not be allowed to continue to intimidate future generations. Massive as these weapons are, they are slow and no match for our lightweight DDD techniques &#8211; we will lure them into shallow memory and watch them go aground, tangled in their own distributed transactions.

For now, though, our troops have withdrawn to the safety of our own home OSGi modules, where order, structure and modularity reign supreme.

Stay tuned for future reports&#8230;.

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