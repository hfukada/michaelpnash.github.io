---
title: Headlights and Guardrails
author: mnash
excerpt: 'In software development, we want to go as fast as possible - and no faster. The real trick is the "and no faster" part, as knowing how fast you can go without suffering either rapidly accumulating code debt or other nasty things is often the least understood part.'
layout: post
permalink: /headlights-and-guardrails/
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
tags:
  - Agile
  - design
  - guardrails
  - headlights
  - quality
  - testing
---
<table border="0">
  <tr>
    <td>
      <img src="http://50.116.19.42/wp-content/uploads/2009/05/road-at-night.jpg" alt="road at night Headlights and Guardrails"  title="Headlights and Guardrails" />
    </td>
    
    <td>
      In software development, we want to go as fast as possible &#8211; and no faster. The real trick is the &#8220;and no faster&#8221; part, as knowing how fast you can go without suffering either rapidly accumulating code debt or other nasty things is often the least understood part.</p> <p>
        Why do we want to go fast in the first place? Well, if we&#8217;re not accumulating technical debt, our quality is still within the bounds we&#8217;ve set for ourselves, and we&#8217;re satisfying user stories, then we want to be able to accomplish as much as we sustainably can each sprint. This way we can deliver value faster, and people tend to like to pay for that kind of thing <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Headlights and Guardrails" class="wp-smiley" title="Headlights and Guardrails" />
      </p>
      
      <p>
        Well, first, we need a road: the basics of an agile environment need to exist before we can go very fast at all. If we&#8217;re working on the build system every sprint and trying to get the basics of a story understood, we&#8217;re still in road construction, and we shouldn&#8217;t expect much in the way of speed until we get some of this basic asphalt laid down and smooth. These includes such basics as a good development setup for our team, a basic understanding of agile principles and a grasp of the technology stack we&#8217;re using, and the support of a continuous integration server, to mention a few. If we&#8217;re attempting to bounce along over the potholes without setting up a proper environment for rapid delivery of software value, we&#8217;ll reap what we sow.
      </p>
      
      <p>
        Assuming we&#8217;ve built the road, then, what things tend to hold us back? Just like on a real road, the only things stopping us from going faster and faster (to the mechanical limit of our vehicle, or in our case, our keyboards and brains) are either externally-imposed limitations (e.g. a speed limit and cops to enforce it), or our own ability to control the pace without going off the road. In software construction, as in life, we can go off the road in many varied ways, but they all tend to be spectacular, destructive, and painful. Unlike the real road, we can be cruising along for some time before we discover we&#8217;ve left the asphalt behind and are sailing over a cliff. </td> </tr> </table> <p>
          We&#8217;ll start by assuming that our corporate environment has eliminated externally imposed speed limits and political roadblocks &#8211; not always a safe assumption, but lets assume for the moment that we&#8217;re one of the luck developers who work in such a situation.
        </p>
        
        <p>
          Our top-level speedometer, to overuse our analogy a bit, is our velocity, measured in features per iteration, or complexity points per iteration &#8211; in other words, how much business value are we adding per time period?
        </p>
        
        <table border="0">
          <tr>
            <td>
              <img src="http://50.116.19.42/wp-content/uploads/2009/05/dashboard-gauges.jpg" alt="dashboard gauges Headlights and Guardrails"  title="Headlights and Guardrails" />
            </td>
            
            <td>
              Just as on the real road, though, the speedometer alone doesn&#8217;t tell the whole story. If we like the number of feature points were churning out just fine, but we&#8217;re suffering rapidly increasing code debt, defect count, or other &#8220;red lights&#8221;, we won&#8217;t be zooming along at that speed for long before something blows. Some of the other dashboard guages we have to look at are our code coverage, our complexity metrics, our adherence to coding and other standards, and so forth. If we&#8217;re not monitoring all of these, then we&#8217;re not going to know if something is going wrong until smoke starts pouring out from under our metaphorical hood.</p> <p>
                The most common way to go off the road is for quality to slip. This can be detected in one of a number of ways, including an ever-increasing defect rate. If most of your sprint is taken up by fixing defects or paying off code debt, then you&#8217;re probably trying to go too fast (or you&#8217;ve not finished laying the road after all). Of course, it&#8217;s possible you&#8217;ve just got a few bad drivers on your team, but we&#8217;ll assume that&#8217;s easier to see (if not necessarily easier to fix). What&#8217;s worse than seeing quality slip? Not seeing quality slip, even though it is. We can&#8217;t measure quality directly, per se, but we sure can measure a lot of other things. Once we know what the normal position of each guage is (e.g. once we establish reasonable code standards that we can measure), then we can watch them to get early warning of things going awry. </td> </tr> </table> <p>
                  Just like on the real road, we need two categories of things, it seems, to help us go as fast as safely possible: I&#8217;ll call them headlights and guardrails.
                </p>
                
                <p>
                  <strong>Headlights</strong>
                </p>
                
                <table border="0">
                  <tr>
                    <td>
                      <img src="http://50.116.19.42/wp-content/uploads/2009/05/car-headlights.jpg" alt="car headlights Headlights and Guardrails"  title="Headlights and Guardrails" />
                    </td>
                    
                    <td>
                      Headlights are tools tools and techniques that let us see where we&#8217;re going and if we&#8217;re going where we want to be. </p> <p>
                        The most basic tools here are user stories, acceptance criteria/tests (ideally executable ones), and metrics such as defect rate and velocity measurements. None of these are trivial or straightforward, and it&#8217;s easy to think you&#8217;ve got a good view and suddenly discover you&#8217;ve been accumulating code debt without realizing it. The only proper reaction at that point is to slow down and correct the problem, as we&#8217;ll discuss below.
                      </p>
                      
                      <p>
                        A good business understanding of the goals and epics behind our user stories gives us more range to see further ahead, and going fast requires looking further ahead, while at the same time paying attention to where you are at the moment.
                      </p>
                      
                      <p>
                        Just like when driving we must be aware of the road immediately ahead, our user stories give us the close-focus we need to be doing the immediately useful thing. We can&#8217;t discard these in favor of looking further ahead exclusively, or we&#8217;ll never get to where we want, but we <b>can</b> combine that with an awareness of both the near future and an understanding of the overall destination to make better decisions in our day-to-day work. </td> </tr> </table> <p>
                          If we concentrate exclusively on the user stories in hand for each iteration we can find we&#8217;ve lost sight of the forest, and may have a hard time fitting together features that should blend into an overall product. If we concentrate only on the distant horizon and not on the user story we&#8217;re working on we&#8217;ll never get anything done. The proper balance lets us go fast.
                        </p>
                        
                        <p>
                          We don&#8217;t want to be like the driver in the joke with the punch line that ends &#8220;we&#8217;re lost&#8230; but we&#8217;re making bloody good time&#8221;!
                        </p>
                        
                        <p>
                          Looking a bit further ahead also allows us to anticipate curves and obstacles in the road, and be ready to hand them when they arrive. If we know, for instance, from our long-range planning that we intend to scale our application to thousands of users, we might make different decisions than if we&#8217;re aware that a single user on a desktop box is the intended audience &#8211; even though neither of these factors is really represented directly by each user story we work on.
                        </p>
                        
                        <p>
                          Executable acceptance tests from a tool like Greenpepper, Fitness, RSpec, or the like can be valuable headlights, freeing developer time from the repetitive manual verification and allowing BA/Customer Proxies to have control over the acceptance process &#8211; again freeing up developers to develop, and maximizing team velocity. As was mentioned in a recent stand-up meeting: if you&#8217;ve manually tested once, you&#8217;ve probably already spent more time than it takes to set up an automated test to do the same thing repeatedly, not to mention you&#8217;ve probably enjoyed it a lot less <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile Headlights and Guardrails" class="wp-smiley" title="Headlights and Guardrails" />
                        </p>
                        
                        <p>
                          <strong>Guardrails</strong>
                        </p>
                        
                        <table border="0">
                          <tr>
                            <td>
                              <img src="http://50.116.19.42/wp-content/uploads/2009/05/safety_guardrails2.jpg" alt="safety guardrails2 Headlights and Guardrails"  title="Headlights and Guardrails" />
                            </td>
                            
                            <td>
                              Guardrails are things that give us some path to follow, and, if necessary, make an ugly noise if we stray too far from that path. They include our basic test suite (and the ugly noise of a build breaking when we hit the rail), as well as coverage and other analysis tools.</p> <p>
                                There&#8217;s a big difference between guardrails and a stone wall built across the road ahead, however &#8211; it&#8217;s not hard to let a testing tool or technique turn into a straightjacket, with tons of brittle and hard-to-maintain tests that don&#8217;t help us at all. We need the right tool for the right job, and used the right way.
                              </p>
                              
                              <p>
                                If we have guardrails ensuring the basics of our code quality, we can go faster with the confidence that when we look back at the end of each sprint we will not have accumulated more code debt that needs to be paid back later. For example: if we establish a test coverage metric that ensures we have a breaking build if our code coverage goes below a certain minimum level (I propose this always be 100%, but that&#8217;s another post), we can move forward with the assurance that there&#8217;s no code that&#8217;s being left untested, so we won&#8217;t find ourselves in the distinctly non-TDD-like position of having to go back and write tests for existing code, burning time that should be able to be used for the next story.
                              </p>
                              
                              <p>
                                We can also refactor with better confidence if we know for a fact there are tests watching over our shoulders, ready to break should our refactor not be true. Refactoring code that is, at least in part, untested should always be an unacceptable risk.
                              </p>
                              
                              <p>
                                If we have some checkstyle, PMD, FindBugs or other static analysis tools checking that our cyclomatic complexity is within bounds, that our class size and line length are readable, and other critical maintainability and coding standards factors are met, we can plunge forward without the fear of a huge cleanup being required just to make the code understandable down the road a ways. </td> </tr> </table> <p>
                                  Of course, just like guardrails and headlights are not infallible in the real world, all the tools and checks in the world don&#8217;t ensure good quality code. One area that&#8217;s particular hard to ensure quality within via automatic mechanisms is design. You can have code that&#8217;s 100% covered, passes every checkstyle rule known to man, and still represents a terrible design. This is where the human factor comes into play &#8211; the automation merely ensures that you&#8217;re spending valuable human attention span on the stuff that really requires a brain, as opposed to things that can be verified mechanically.
                                </p>
                                
                                <p>
                                  Discipline is the glue that makes all of this work together &#8211; often times developers themselves will have the &#8220;smell&#8221; of something done not quite right, but not feel like they&#8217;ve got the latitude to dig into it and clean it up, so they save it until the mythical &#8220;later&#8221;, which sometimes never comes. Management and team leads must also be disciplined enough to have the patience while that kind of refactor happens &#8211; with the firm knowledge that they&#8217;ll get paid back by better productity and a lower defect rate over the mid to long term.
                                </p>
                                
                                <p>
                                  A final warning: It&#8217;s easy to let headlights become leashes and for guardrails become cubicle walls. Many agile practitioners are concerned, and rightly so, that adding tools and techniques can turn into a new dogmatism and inflexible methodologies. It&#8217;s up to us in the trenches to make sure we don&#8217;t let this happen, while at the same time getting all the juice we can out of helpful techniques and tools.
                                </p>
                                
                                <p>
                                  Properly applied, though, headlights and guardrails can be valuable tools in letting us reach our maximum velocity, while still arriving safely at our destination.
                                </p>
                                
                                <div class="g-plusone" data-annotation="inline" data-width="300">
                                </div>
                                
                                <p>
                                  <!-- Place this tag after the last +1 button tag. -->
                                  
                                  <br />
                                </p>
                                
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