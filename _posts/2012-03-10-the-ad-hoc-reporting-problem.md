---
title: The Ad-Hoc Reporting Problem
author: mnash
layout: post
permalink: /the-ad-hoc-reporting-problem/
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
I&#8217;ve recently had the opportunity to consider the impact on a service-oriented/event-driven architecture of the requirement for &#8220;ad-hoc reporting&#8221;, and I&#8217;d like to share some of my reasoning and conclusions here.

In the last many years, I&#8217;ve built systems that consist of a set of services. These services are used by a web UI and various other client applications to interact with users, load data, process that data in various ways, and export some of that data to other systems.

A fundamental goal of using a service-oriented architecture is to keep the cost of new changes as low as possible. That&#8217;s not the same as going as fast as possible, but it does often result in a high and sustainable pace of change as well. The advantage of this is that it allows the whole organization to respond to changes in the market quickly and without excessive cost. 

That cost is broken into two parts &#8211; the apparent costs, which is the developer and operations time costs to implement and deploy a new feature, and the non-apparent costs, which are the accumulating technical debt of each change. The apparent costs are easy to measure: how many hours, days, weeks did this change take, and how many developers and other staff did I pay to do the change.

The non-apparent costs, relating to technical debt, are much less obvious. This cost is not directly measured in dollars at first &#8211; it is measured in dollars later. The best way to see it is to consider the cost difference per feature over time. Let me use an example to illustrate: Let&#8217;s say that we&#8217;re good at breaking up feature requests into approximately equal-sized pieces, and that the average cost of a feature with a given team is, say $100. If we&#8217;re accumulating no technical debt at all in a given sub-system, then our cost per new feature remains about $100 (not taking into consideration any changes in the cost of talent over time for the moment). 

If, on the other hand, we are accumulating technical debt, then the cost per feature over a few months might rise to, say, $110. Then in another couple of months is $120, then $140, and so on. Each new feature is only worth so much to our business, to look at the other side of the equation. Let&#8217;s say, for the sake of argument, that a given new feature is worth $150 per month more in revenue. Simple economics tells us then that paying $150 for that feature allows it to pay for itself in a single month &#8211; so it makes sense to write it, even if the cost for that feature has risen to $150. 

Unfortunately, it&#8217;s not this simple: the revenue from a feature is not easy to measure or estimate, and it does not remain constant over time &#8211; a shiny new feature might net us $150 more the first month, then $140, then $120… until the shine is gone and it&#8217;s not contributing to our product at all (arguably, that&#8217;s the time to take it out again, but that also costs money &#8211; and it&#8217;s hard to know).

It also matters, often a lot, WHEN a new feature is released. We might gain $150 profit from a feature if we release the month before our competition, but it might be worth much less after everyone else has it. In fact, we might still need our new feature just to keep up with the joneses &#8211; we might have to pay to develop it despite no increase in profit, we might need it just to avoid losing customers to the competition.

We can make a number of observations here. It is clearly desirable to get each new feature for as low a cost as is sustainable &#8211; that is, we&#8217;d like to keep paying about the same per feature over time. At the same time, we have to carefully select where we spend our money per feature so we have the right feature at the right time in order to maximize our revenue &#8211; this means the time to implement a feature is as important as its cost, sometimes more so. We might be willing to pay more to have a feature sooner, and we must be able to make that decision.

On any given system, it is common for the cost per feature to rise over time. This is due to a number of factors, but a critical one is the underlying design of the system, its level of coupling and cohesion, its indépendance from other systems, etc. The RATE of the increase over time is the most useful measure of the effectiveness of the design &#8211; if it&#8217;s increasing sharply, we may hit what I&#8217;ve called previously a point of &#8220;technical debt bankruptcy&#8221;, where its not financially responsible to add new features, as we can&#8217;t possibly make enough money from them to make it worth the ever-increasing costs.

Increasing costs also make the order of features more critical &#8211; if we get a less important feature done before a more important one, we&#8217;ve increased the cost for the more important one, hastening our collision with the bankruptcy point all the more.

I go through all of this in order to highlight the importance of being able to produce new features sustainably, at a predictable pace and at either a constant or a slowly-increasing cost. The delta over time of the average cost per feature is one good metric of the technical debt &#8211; often, some non-feature work and refactoring can in fact reduce that delta, at least for a while, so we sometimes see a pattern of bursts of new features, then a slower period where we &#8220;pay down&#8221; some of that debt, then go again, without letting it get out of hand. This is also a sustainable pattern.

Creating new features more rapidly, with less thought to design and architecture, looks good at first &#8211; we get features more rapidly, and for an apparently low cost. The affect on the delta, however, is exponential in this situation &#8211; the next feature doesn&#8217;t cost a bit more, it costs a LOT more, as we&#8217;re having to be constrained by the decisions we made in a hurry last time. That&#8217;s not to say that it&#8217;s not sometimes the right decision to go fast, and to acknowledge that we&#8217;re accumulating technical debt. 

The mistake that I&#8217;ve seen over and over again, however, is to disavow the existence of the delta, of the cost of technical debt entirely. To not take it into account when making decisions is to make decisions without all the facts.

One of these decisions is the difference in importance between various design and architecture decisions, such as service-oriented architectures and event-driven architectures. One of the primary features of a well-crafted SOA/EDA is the ability to decouple systems &#8211; by this I mean that changes and new features in one system do not necessitate changes and impact on another. You can change your customer-relation-management system and its features without breaking (or even affecting) your shopping-cart system, for instance. This means that the overall cost of the change to your CRM is lower, as you don&#8217;t need to take into account the fact that you&#8217;ll break the shopping-cart &#8211; or any other system.

One of the ways that SOA/EDA creates this advantage is by specifying the communication between systems &#8211; the CRM, for instance, might respond to events from the shopping cart when customers buy things. It has no idea how the shopping cart works, or what its process for selling is, it only knows the well-defined API between it and the cart, whether this be events, REST calls, or some other mechanism &#8211; the main thing is that one system does not &#8211; in fact, must not &#8211; know the &#8220;internals&#8221; of the other. 

This is true in good system design in general, not just in a SOA architecture. When designing with objects, for instance, there is the concept of &#8220;information hiding&#8221;, where the internal details of the implementation of even a single object are not exposed carelessly to the outside world. They are, instead, exposed only through carefully crafted interfaces, e.g. an API. The idea scales up to entire services just the same.

So, you might by now ask, what does this have to do with ad-hoc reporting? 

Ad-hoc reporting has traditionally relied on access directly to a persistent store of some kind, typically a relational database, to be able to produce reports and replies to queries that were not anticipated when the system was built (hence the ad-hoc part). In order to do this, and to formulate a meaningful report, the report creator has to understand the meaning of the stored data, especially how it relates to other stored data, so that sets of data can be joined. This means that the domain design must be represented not in the logic of the application, but in the schema of the database. Not just the logic of one domain, or one service, either, but the logic of any that you wish to join together for ad-hoc purposes.

Good service-oriented architecture that relies on an API treats persistence as an internal implementation detail of the service &#8211; e.g. it&#8217;s the service&#8217;s business, and its alone, how it manages to store its data. Whether it&#8217;s in a database, a file, or in some kind of magical cloud storage doesn&#8217;t matter at all &#8211; and MUST not matter at all &#8211; to the clients of the service, or we&#8217;ve lost a key advantage.

But what is to stop a service from simply storing its data in a manner that can in fact later be used by ad-hoc tools? Where&#8217;s the harm, you might ask?

The harm is what brings us back to the discussion of technical debt again. 

Let&#8217;s say we design our CRM service to store its data in a nice relational database, so we can support ad-hoc queries later. Now we leave the CRM service and go to the shopping cart service &#8211; same thing, we should store our data in a nice normalized schema, so we can later come along with SQL and do our queries. 

Right away we&#8217;ve made some fatal assumptions: the domain model must now be entity-based, in order for ad-hoc queries to be meaningful. What I mean is this: Let&#8217;s say in our shopping cart we decided to create our customer domain object from a series of &#8220;customer-edit&#8221; events. Our service stores the events, and uses the CQRS pattern to create the customer domain object from the event entities. How do we get a list of customers from our ad-hoc reporting tool? Well, we&#8217;ve got two choices &#8211; either create the customer in some kind of view, essentially duplicating the logic that creates the customer domain object in the service, or don&#8217;t store the customer that way &#8211; store the customer as the completed domain object, or a relational representation of that object (as a customer is rarely &#8220;flat&#8221; in practice).

Now we&#8217;re seeing where the decision to design for ad-hoc reporting is skewing our service design &#8211; it&#8217;s making us consider doing things in a non-optimal manner in order to keep the world in a state where ad-hoc reporting can operate, and causing us to &#8220;bleed&#8221; domain knowledge from our service into a database schema.

Let&#8217;s say we&#8217;re OK with that decision, that we don&#8217;t mind losing a bit of design freedom in order to have our reporting choices. 

Now let&#8217;s consider the CRM service. It also deals with customers, and might also have used some kind of event architecture to do its work. Let&#8217;s put it in a relational database as well, and structure its schema so we can do our reporting. It is very probable that the customer we&#8217;re dealing with in the shopping cart is the same customer (conceptually) as we&#8217;re dealing with in the CRM. Ok, then we&#8217;d like to be able to join between these two elements, and produce ad-hoc reports. This means that the CRM system must share a data definition of the key of the customer table with the shopping-cart system &#8211; e.g they must agree on data-type, and on length, and on the way the key is produced, etc.

Now we&#8217;ve started coupling these applications: any change to the customer key in CRM means a corresponding change to the customer key in the cart. Well, at that point, why don&#8217;t we just merge the two tables and have just a single definition of customer? Wouldn&#8217;t that be simpler? At first blush, it certainly seems so. Ok, now we&#8217;ve coupled a bit further, essentially making CRM and shopping cart into a single system. Where&#8217;s the harm? This brings us back to technical debt. A change to the CRM now means we must consider the impact of that change on the shopping cart, increasing the cost of that change. How much? It&#8217;s hard to say, it depends on the change, but this is a simple example &#8211; this pattern leads the way to the &#8220;big ball of mud&#8221; design, where you essentially have a single database for all services, at which point the temptation to simply use the database as a means of communications between applications becomes too great &#8211; and once you&#8217;ve done this, you don&#8217;t have lots of small applications, you just have a single application, one giant monolith that is nearly impossible to maintain, with exponentially increasing costs per change.

Another cost must be taken into consideration as well &#8211; when the ad-hoc reports are created, they are of course created at a point in time, and the schema of our mega-app is at a certain point. As the schema changes (and it will, albeit more slowly over time, as it becomes too expensive to consider easy schema changes), the ad-hoc reports, for which we went to all this trouble, stop working. I&#8217;ve never seen a &#8220;one-time&#8221; report that didn&#8217;t get saved and run over and over again, and every time the schema changes, this report breaks, and the user who used the &#8220;easy&#8221; reporting tool comes screaming down to find a developer to help him fix his report.

What we&#8217;ve essentially done is created another application: ad-hoc reporting. It is every bit as bound to the schema as all the other apps, and requires as much, perhaps more, maintenance over time. The perceived &#8220;savings&#8221; of having users do their own reports is eventually lost altogether, and is usually a net loss, costing more than if the users simply requested reports via the APIs of the services in the first place (even though that takes developer time to create).

This doesn&#8217;t happen all at once, of course. An expert team of developers that moves in this direction can manage it quite well, at least for a while. When the pressure to develop more features more quickly increases, however, it&#8217;s common that less experienced developers will start to introduce subtle couplings, that go unnoticed until you try to go fast, then suddenly something breaks.

The logical end of this pattern is to put more and more of the &#8220;logic&#8221; of the mega-app into the database, first in the schema, by having richer and richer &#8220;domain&#8221; objects stored (for instance, adding an &#8220;account total&#8221; field to the customer because it&#8217;s easier than adding it up every time &#8211; then when the logic to add it up changes in the app, it must change in the database as well). This then leads to the madness of stored procedures and triggers, as we try to &#8220;program&#8221; the anemic domain model of the database. At this point, costs per new feature are astronomical, the bug rate is through the roof, and I usually get called as a consultant <img src="http://jglobal.com/wp-includes/images/smilies/icon_smile.gif" alt="icon smile The Ad Hoc Reporting Problem" class="wp-smiley" title="The Ad Hoc Reporting Problem" /> 

There are actually other losses that I&#8217;ve not even detailed when we move towards a shared schema: The rapid and ever accelerating cost increases of a shared schema is only the most visible. The subtle costs of making your developers have to think more about each and every schema change are perhaps, in the long run, worse. For instance, if I&#8217;m working on a service and I know that the only thing that uses its persistence mechanism is that service, I can tune the persistence for maximum advantage &#8211; I don&#8217;t have to worry about all the other use-cases of that store, there aren&#8217;t any. If I want to change the schema, I don&#8217;t have to form a committee, as long as the service continues to pass its integration tests, I can change it all I want, now, right away, and in as radical a manner as I need. This is one reason that developers love post-relational database systems such as MongoDB and Cassandra. It&#8217;s almost effortless to change the schema, as it&#8217;s defined in your application code, where it ought to be. If the domain design is only the business of the application, then where else would it be? If the domain, on the other hand, is shared between many applications, or even two, then I immediately have artificial constraints on change, which increases cost and decreases velocity. Key-value/post-relational databases also avoid that horrible impedance mis-match we call object-relational mapping layers, which are again an impediment to design freedom and easy change. Schemas that are shared and are outside the application have a tendency to fossilize &#8211; they become so hard to change that in the end we don&#8217;t change them at all, and make poor choices in our applications to &#8220;work around&#8221; their inadequacies, further reducing quality, increasing cost and time.

What are the alternatives to this scenario? How can we build systems to support the need for reporting without dissolving into a ball of coupled goo? Are these goals mutually incompatible?

First, it&#8217;s a false economy to say that we&#8217;ll design for easy ad-hoc reporting to save the time for developers to write reports: As we&#8217;ve seen, if we make the system coupled and schema-transparent enough to make it easy for power users to write reports, we&#8217;ll waste far, far more developer time than if we just admit we have a requirement for reporting and put it in the backlog. To think there&#8217;s a &#8220;cheap&#8221; way to get decent reporting is to defy reality &#8211; there just plain isn&#8217;t, and we should be professional enough to admit it. 

If we&#8217;re ok with a tightly coupled system that costs a lot to change, but that support easy ad-hoc, that&#8217;s fine, let&#8217;s make that tradeoff and be upfront about it.

What if we want our cake and to eat is as well, is there any middle ground? Sure there is, and it&#8217;s the same one that&#8217;s been around for decades: it&#8217;s called a data warehouse.

Given enough access to the APIs of the services that make up our decoupled SOA/EDA-driven system, it&#8217;s straightforward to build a simple data warehouse optimized for ad-hoc queries. What we&#8217;re really doing is building a new set of clients to our services that have a different read model &#8211; this time, the read model is optimized for reporting. We build this warehouse one of two ways: where events exist that have the data we need, we listen to those events and build, where no events exist we execute timed batch jobs that query APIs &#8211; no, not the underlying database, the API &#8211; and write the results into our warehouse.

The warehouse is NOT the authoritative source of the original data, and that&#8217;s a good thing. It means we can produce a consistent and meaningful view of the data, which is not possible when reading directly from our production database (as it&#8217;s always changing and may be inconsistent at any given time). We also avoid any potential performance impact on production system, or, worse, locking tables with a read lock if we&#8217;re trying to get consistency and blocking readers and writers in the production system. You can index the data warehouse to optimize reads, which might be exactly the opposite of what you want in your production data stores.

Often the data warehouse is done with a relational database, even if the production data stores are not. For one, this gives the freedom to choose the best persistence technology for the job when building services, which contributes to cost savings, but it also speaks to the relative maturity of tools for querying in an ad-hoc manner available for relational databases. Although some tools exist for doing the same in the post-relational world, they&#8217;re not as mature as their relational cousins.

Is this data warehouse technique some work? &#8211; yes, of course. Is it worth it? I believe so quite firmly, yes. This work can be done without impacting the services and features being built for production at all.

You get the advantage of exactly the schema you want for ad-hoc purposes, even if that schema is only loosely related to the entity designs that the source data services use. You don&#8217;t have any impact at all on the services that comprise your production system, either in design or in performance, at any time. You control and have visibility as to the amount of time, money and resources that are going in to supporting ad-hoc reporting, so you can make informed decisions on how much to spend, instead of hiding those costs where they&#8217;re just as real, but much harder to see.

Conclusion

SOA and EDA are not just the new shiny thing, the latest fad. They are a fundamentally different and better way of building systems.

They are techniques which are exactly opposed to the idea of shared databases, anemic domains, and externalized fossilized schemas. Attempting to shoehorn those attributes into a SOA/EDA architecture results in many, if not most, of the advantages of SOA/EDA being lost, and the resulting frankenstein is simply bad software, costing more to develop and maintain than the advantages are worth.

If what you want is ad-hoc reporting capability, be honest about it, call it a feature, and build it into your system without compromising your design integrity and costing far more in the medium to long term. Anything else is simply unprofessional, in my opinion.

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