---
title: I have seen the Futures
author: mnash
layout: post
permalink: /i-have-seen-the-futures/
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
  - Uncategorized
tags:
  - Actor
  - Concurrency
  - concurrent
  - futures
  - java.threads
  - parallel
---
Java has always had the ability to develop concurrent applications &#8211; right from the start, the &#8220;Thread&#8221; class and its kin gave a single Java application the power to spawn off a separate process, while continuing with the original process. Like all concurrency, it was of course limited by the amount of cores or systems available to run processes, but the basics were there.

More recently, however, it&#8217;s become clear that higher levels of concurrency are required in order to make our applications as scalable as we&#8217;d like, especially in light of recent hardware trends that give us not as many huge leaps upward in terms of speed, but provide more and more cores for our applications to spread themselves into in each system.

Concurrency is more than running multiple processes on the one box, though &#8211; we must think of the problems we&#8217;re trying to solve in new ways, ways that lend themselves well to expressing groups of smaller tasks that can all be happening at once, with as little temporal dependency as possible &#8211; that is, trying to reduce the need for one task to wait for another task to complete before it can move ahead. This is not just a programming issue, it has to be taken into account at design-time as well, to a degree.

Java&#8217;s original concurrency support was oriented more towards richer threads &#8211; entire streams of execution that could exist for a long time if needed. Just the thing if you&#8217;re writing a web server, or something similar. These richer threads were expensive to create, however, so a developer didn&#8217;t want to just spin off thousands of them, or the hope-for increase in scalability would be lost to the overhead pretty quickly.

Other problems lend themselves better to a lighter-weight kind of concurrency, where the cost of breaking up into smaller concurrent tasks is lower, and the tasks generally shorter-lived and less complex than a full thread. This leads us to lightweight alternative methodologies such as Fibers, Processes, and Actors, such as those found in more functional-oriented languages, such as Haskell, Erlang and others.

In more recent incarnations of Java, libraries were added to the JDK to allow us to do quite a bit of lightweight concurrency right in good ole&#8217; fashioned Java, however, and these bear closer inspection if you&#8217;re not familiar with them.

Let&#8217;s take a closer look at java.util.concurrent and it&#8217;s classes by way of a code example&#8230;

Let&#8217;s say we&#8217;ve got a class to do some useful piece of work, say a piece of mathematics, that takes some time to process. Let&#8217;s call it &#8220;UsefulWork&#8221; in a fit of creativity. It&#8217;s created with a parameter that gives it what it needs to do the useful thing it does &#8211; in our example, just an integer.

We have a lot of these classes to run in order to solve our overall problem, each with a different set of parameters. When we&#8217;re all done, we need to add up the results and present the final answer to our caller.

In the sequential world, we might defined our UsefulWork process as a simple method, like so:

<pre class="prettyprint lang-java linenumstrigger linenums">private long doUsefulWork(int param) {
    ... do the number crunching...
    return result;
 }
</pre>

and we might call this method a bunch of time, once with each of our parameters, adding up the overall result as we go, like thus&#8230;

<pre class="prettyprint lang-java linenumstrigger linenums">long finalResult = 0L;
for (int i = 0; i &lt; numberOfJobs; i++)
   finalResult = finalResult + doUsefulWork(param[i]);
}
</pre>

Each computation complete, we add up our answer, and life is good. But if we look at this problem in a different way, there&#8217;s nothing about each call to doUsefulWork that requires the answer from the previous call &#8211; each one does it&#8217;s job independently. So what&#8217;s stopping all the useful work from happening *concurrently*, rather than one piece at a time? Not a thing &#8211; let&#8217;s see how that would look.

Instead of a method, we now define a little class to do our useful computation for us, while implementing the Callable interface, like this:

<pre class="prettyprint lang-java linenumstrigger linenums">private class UsefulWork implements Callable&lt;Long&gt; {

       private int param = 0;

        public UsefulWork(int param) {
            this.param = param;
        }
        @Override
        public Long call() throws Exception {
            ... work out the result, using the param, however it is we do that....
            }
            return amount;
        }
    }
</pre>

The &#8220;call()&#8221; method is defined in the Callable interface, and is a bit like the &#8220;run()&#8221; method from Thread, except it allows us to return a result.

Now we tee up a series of our UsefulWork classes, like so:

<pre class="prettyprint lang-java linenumstrigger linenums">List&lt;UsefulWork&gt; usefulWorkList = 
        newArrayList(new UsefulWork(100), new UsefulWork(50), new UsefulWork(200), new UsefulWork(10),
        new UsefulWork(500), new UsefulWork(125), new UsefulWork(80));
&lt;/code&gt;
</pre></div> 

(we&#8217;re using a method from the invaluable Google Collections library to spin up a new ArrayList of the proper type here)

Now we fire up our new Callables like so:

<pre class="prettyprint lang-java linenumstrigger linenums">ExecutorService executorService = Executors.newFixedThreadPool(POOL_SIZE);
List&lt;Future&lt;Long&gt;&gt; futures = executorService.invokeAll(usefulWorkList, 5, TimeUnit.SECONDS);
Long total = 0L;
        for (Future future: futures)
            total = total + (Long) future.get();
</pre>

In the first line above, we create an ExecutorService, in this case, using a fixed-size &#8220;pool&#8221; of threads which will be used to run our jobs (this is the expensive bit, so it&#8217;s nice to do this in some kind of initialization only once &#8211; the same pool can be re-used).

Then we create a list of Future objects, each of which deals with type &#8220;Long&#8221;, by calling the executorService.invokeAll. The parameters are our list of Callables, timeout, and the unit in which the timeout is expressed &#8211; in this case, seconds. What we&#8217;ve said is &#8220;start doing all these things I&#8217;m giving you at once, but don&#8217;t allow any one of them to run more than 5 seconds&#8221;. We can also use unlimited timeouts, but then a hanging Callable can get us in trouble.

The rest of our code above is just collecting the results &#8211; once we&#8217;ve made the call to &#8220;invoke&#8221; our UsefulWork&#8217;s are all churning away (POOL_SIZE of them at a time, anyway), doing whatever they do to get their invdividual answer without waiting for the herd.

Our for loop at the end simply collects the fruit of their labours, retrieving the results of the calculations that have already been performed. It&#8217;s important to note that the call to &#8220;get()&#8221; is *not* actually doing the calculation at that moment &#8211; the actual calculation is already finished, ready to return. This is the power of the Future interface &#8211; the ability to do it&#8217;s job and then be available at a later time for retrieving the result.

This is of course an extremely simple example, and doesn&#8217;t take into account several things you might need to think about for real production code, but I think it gives a taste of what&#8217;s possible just with what comes with the standard JDK.

In a later post we&#8217;ll lean on java.util.concurrent a bit harder, and see what other things we can do.