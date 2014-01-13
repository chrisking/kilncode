---
layout: post
title:  "Robust and Resilient, Do They Lead to Antifragile Software?"
date:   2014-01-12 18:59:03
tags: software engineering, systems theory, antifragility, resilient, robust yet fragile
author: Chris King
---

## Intro

In the field of software engineering, we as developers are always striving for improvements in our process of building software. We seek to improve the total throughput of our systems, their scalability to performance demands, and the clarity of the codebase. During this search, countless methodologies have been created (Test Driven Development, Agile, Waterfall, Domain Driven Development, Behavior Driven Development, etc), all of which are constantly evolving and changing due to research in our own field, and in others such as behavioral economics, complexity theory, and systems theory.

The key to understanding and learning from any discipline is clear communication of the ideas and concepts that are being discussed. This article aims to illustrate ways in which a few developers have misinterpreted the research on antifragility, and then to properly tie what our discipline is doing to achieve robust and resilient systems, and how antifragility does not make sense as a goal.

The concepts of fragility, robustness, resilience, and antifragility are useful models to classify the strengths and weaknesses of a system. By understanding these concepts we can hope to identify how much we should rely on our applications and what we can do to improve our applications.

## What is Antifragile?

In Nassim Nicholas Taleb's "Antifragile" he defines antifragile as: "beyond resilience or robustness. The resilient resists shocks and stays the same; the antifragile gets better." [excerpt](http://www.fooledbyrandomness.com/prologue.pdf) He continues, helping us identify objects as antifragile or not:

> "It is far easier to figure out if something is fragile than to predict the occurrence of an event that may harm it. Fragility can be measured; risk is not measurable (outside of casinos or the minds of people who call themselves “risk experts”). This provides a solution to what I’ve called the Black Swan problem—the impossibility of calculating the risks of consequential rare events and predicting their occurrence. Sensitivity to harm from volatility is tractable, more so than forecasting the event that would cause the harm. So we propose to stand our current approaches to prediction, prognostication, and risk management on their heads. In every domain or area of application, we propose rules for moving from the fragile toward the antifragile, through reduction of fragility or harnessing antifragility. And we can almost always detect antifragility (and fragility) using a simple test of asymmetry: anything that has more upside than downside from random events (or certain shocks) is anti- fragile; the reverse is fragile."

In the above snippet Taleb references his earlier work on [Black Swans](http://www.amazon.com/The-Black-Swan-Improbable-Robustness/dp/081297381X/) and proposes that the goal of antifragile entities is to withstand Black Swan events when they arise and to be made better by them. The criteria as defined by Taleb for a [Black Swan](http://en.wikipedia.org/wiki/Black_swan_theory#Identifying_a_black_swan_event):

1. The event is a surprise (to the observer).
2. The event has a major effect.
3. After the first recorded instance of the event, it is rationalized by hindsight, 
as if it could have been expected; that is, the relevant data were available but 
unaccounted for in risk mitigation programs. The same is true for the personal 
perception by individuals

Before continuing it would be useful to define all of the core terms and how they will be used through this article:

* Fragile - (of an object) easily broken or damaged [Merriam-Webster](http://www.merriam-webster.com/dictionary/fragile)
* Resilient - The capacity of a system, enterprise, or a person to maintain its core purpose and integrity in the face of dramatically changed circumstances. [Resilience p7](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431)
* Robust - A system or entity that has been hardened so that it is not easily broken, while lacking the recovery abilities of a resilient system. [Resilience p13](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431)
* Antifragile - "Beyond resilience or robustness. The resilient resists shocks and stays the same; the antifragile gets better." [Antifragile](http://www.fooledbyrandomness.com/prologue.pdf)

Given how many people have struggled with fragile software, antifragile software seems like an amazing goal to have, but what would that actually look like? Can code actually become stronger when chaos and failures are hurled at it?

## Antifragility and Software

With antifragility established as a goal to strive for, many developers who read Taleb's book started to float around the idea of antifragile software, or software that becomes more powerful when a Black Swan arises.

In Vikas Singh's blog post [Anti-fragile Software](http://scn.sap.com/community/abap/blog/2013/12/01/antifragile-software) he begins with the definitions for fragility, robustness, and antifragility, then proceeds to discuss how software has been stuck in the mindset of robustness being the end goal.

Singh's definitions as mentioned above( *these may be confusing* ):

* Fragile : This is something that doesn’t like volatility. An example will be a package of wine glasses you’re sending to a friend.
* Robust : This is the normal condition of most of the products we expect to work. It will include the wine glasses you’re sending to the friend, our bodies, computer systems.
* Antifragile: These gain from volatility. It’s performance thrives when confronted with volatility.

Singh later writes of the challenges with building more fault tolerant systems:

> "Traditionally we have been designing software systems trying to make them robust and we expect them to work under all conditions.This is becoming more challenging as software is becoming much more complex and the number of components is increasing."

Within a few paragraphs he then makes the following statement: 

> "We spend a great deal of effort in making a system robust but [not] much in making it antifragile.The rough equivalent of antifragile is resilience in common language - it is an attribute of a system that enables it to deal with failure in a way that doesn’t cause the entire system to fail."

Referring to the earlier definition from Taleb we see that antifragility MUST be beyond resilience, and as Singh's work continues, the only solutions brought forward simply increase resilience or robustness, not antifragility at all.

Singh's solutions that will be discussed later:

* Create fault tolerant applications
* Regularly induce failures to reduce uncertainty

So what would antifragile software actually look like? Ideally it would be a system that meets all the criteria for a robust and resilient system yet it should also be able to dynamically change itself and all of its metrics autonomously. These types of systems have been created but are incredibly complex and generally fall out of the purview of most applications, such as spell checking algorithms and random ranking algorithms. These specialized algorithms do not encompass the mission of the software that most developers spend their time writing, this article will focus on the majority of software being created, not the outliers.

## Finding Fragility

The journey towards a robust and resilient application starts with understanding how software can be fragile, and how to buffer it from fragile to robust. Below is a simple Python example of a function to illustrate fragility.

```python
def add_numbers(numbers):
    """
    takes in a simple array of numbers. It will then iterate over each number,
    while doing so it adds the numbers together, finally it returns the result.
    """
    sum = 0
    for number in numbers:
        sum += number
    return sum
```

If the array of integers [1,2,3] is passed, this function will output 6, as expected. Surprisingly Python even handles [1.99,2.5,3.0] correctly yielding 7.49. However if ["one", "two", "three"] is supplied an exception is thrown. Specifically "TypeError: unsupported operand type(s) for +=: 'int' and 'str'" 

Providing unit tests would help prevent a developer from checking an error like this into production as the test would fail. That solution is not antifragility; it is plain robustness. If code using this function was checked into the codebase with incorrect inputs that caused a failure, the code would not become stronger during the failure, it would simply fail. That is not antifragility at all, that is robust yet fragile.

## Robust Yet Fragile (RYF)

Robust Yet Fragile is a term used to describe systems that are resilient in the face of anticipated dangers, but highly susceptible to unanticipated threats. This term was coined by California Institute of Technology research scientist John Doyle.[Resilience p27](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431)

Our world is filled with examples of RYF systems. Those who deal daily with anticipated issues like the electrical grid can handle many isolated failures, but if the failures start to cluster, this will yield a widespread power outage for many. A software example of RYF could be a web application that is served by 2 servers in a simple failover configuration. If both nodes experience a failure, the service will be knocked offline.

RYF is easy to achieve with software, and is certainly a great starting point for a service, but what can we do to enable an application to actually be resilient?

## Resilient Software

The path to producing resilient software starts with identifying how one can leverage the tactics of "Sense, Scale, and Swarm."[Resilience p61](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431) Each of these tactics open up feedback loops, or channels for communication so one's application and those who support it can know more about what is really going on. Once the feedback loops have been established, it should be easy to identify metrics which indicate how the application is performing. 

For this example we will use a web application and illustrate how leveraging technology from [Amazon Web Services](http://aws.amazon.com/), [New Relic](http://newrelic.com/), or [Open Stack](http://www.openstack.org/) can help facilitate the feedback loops of sense, scale, and swarm.

Just as one relies on one's senses before performing many actions, the other steps of scaling and swarming cannot be performed intelligently without sensing exactly how things are changing in ones application. Using monitoring services like [New Relic](http://newrelic.com/), application developers can sense when performance impacting conditions are occurring. Such conditions could be a simple traffic spike, memory leaks, infrastructure failure, or a simple bad new deployment. With real time performance metrics constantly available, it becomes easy to quickly identify the cause of new problems and to determine how best to react to them.

Scaling can often resolve many sudden traffic spikes or resource issues, and with [AWS](http://aws.amazon.com/) or 
[Open Stack](http://www.openstack.org/) is easy and in many cases can be fully automated based on information from the sensing infrastructure. In AWS this is called Auto Scaling and more can be learned from their [official documentation](http://aws.amazon.com/autoscaling/).

Focusing on the important metrics via sensing and increasing the supply of computing power or talented developers in scaling, the only remaining thing is intelligent usage of that information. The intelligent usage of these pieces of information and the combination of resources towards tackling a problem is swarming. Netflix is a well-known example of using continual swarming behavior to ensure their service operates as intended. 

A few years ago Netflix started a program called [Chaos Monkey](https://github.com/Netflix/SimianArmy), this tool lets Netflix test its ability to sense, scale, and swarm automatically by destroying virtual machines running core bits of Netflix's infrastructure. With random small pieces of their production infrastructure being constantly removed they could quickly see which pieces of their infrastructure could heal itself automatically and which pieces needed more work. The program was incredibly successful in helping Netflix reduce downtime and they have extended it since then to many more specialized chaos inducing applications. An even more destructive entity has also gained a bit of popularity called [Chaos Gorilla](https://github.com/Netflix/SimianArmy). Like its monkey counterpart it deletes components of the Netflix infrastructure but instead of just virtual machines it simulates the outage of entire availability zones. A full list of their simian agents can be found [here](http://techblog.netflix.com/2011/07/netflix-simian-army.html). When the infrastructure of an application can take the removal of an entire geographic region of servers and continue to operate as intended, it is safe to say it is truly a resilient application.

As aforementioned, Singh said the two components of an antifragile software entity are fault tolerance and regular induction of failures. Here we see that Netflix has accomplished this and is still vulnerable to a Black Swan event, so while resilient, it is not antifragile yet.


## Conclusion

Antifragile pieces of software that are self modifying may become more commonplace in the future as artificial intelligence methods improve but we seem to be far from those methods now. Until then, resilience provides the best means of ensuring the continued success of our products. Even if a Black Swan should arise and destroy the industry the application exists for, it does not necessarily matter. The skills to understand problems are in the heads of developers, and the lessons learned building a resilient platform can be utilized to build whatever software this new world demands. In that way we as developers are certainly antifragile ourselves, even if our software is not.

### Further Reading: 

##### Antifragile:

1. [Antifragile: Things That Gain from Disorder - Nassim Nicholas Taleb](http://www.amazon.com/Antifragile-Things-That-Gain-Disorder/dp/1400067820/ref=sr_1_1?ie=UTF8&qid=1388748417&sr=8-1&keywords=antifragile)

##### Resilience:

1. [Resilience: Why Things Bounce Back - Andrew Zolli & Ann Marie Healy](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431)

##### Advocates for Antifragile Software

1. [Anti-fragile Software - Vikas Singh](http://scn.sap.com/community/abap/blog/2013/12/01/antifragile-software)
2. [Agile is Antifragile - Stuart Wray](http://onfoodandcoding.blogspot.com/2013/05/agile-is-antifragile.html)
3. [Antifragile Systems: Designing for Agility vs. Stability - Mike Kavis](http://www.virtualizationpractice.com/antifragile-systems-designing-for-agility-vs-stability-22536/)

##### Criticisms of Antifragile (the book)

1. [Fragile Reasoning in Nassim Taleb’s Antifragile: An Enlightenment Transhumanist Critique - Gennady Stolyarov II](http://www.quebecoislibre.org/13/130515-8.html)
2. [Nassim Taleb Is Annoying, but Antifragile Is Still Worth Reading - John Horgan](http://blogs.scientificamerican.com/cross-check/2012/12/05/nassim-taleb-is-annoying-but-antifragile-is-still-worth-reading/)
3. [Anti-Fragile Book: Why We Should Eat Like Cavemen, Embrace Religion, and Hate Bankers - Marni Chan](http://www.policymic.com/articles/19909/anti-fragile-book-why-we-should-eat-like-cavemen-embrace-religion-and-hate-bankers)


