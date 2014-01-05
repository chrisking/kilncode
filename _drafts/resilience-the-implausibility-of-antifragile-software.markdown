---
layout: post
title:  "Resilience, The Implausibility of Antifragile Software"
date:   2013-12-31 18:59:03
categories: software engineering, systems theory
author: Chris King
---

## What is Antifragile?

Nassim Nicholas Taleb defines antifragile in his book "Antifragile" as: "beyond resilience or robustness. The resilient resists shocks and stays the same; the antifragile gets better." [excerpt here](http://www.fooledbyrandomness.com/prologue.pdf) The examples provided for antifragile entities include media pundits, whose reputations don't depend on being correct, and muscles, as they rebound to be even stronger than they were before the stressor was applied.

He continues to later help identify objects as antifragile or not:

> * It is far easier to figure out if something is fragile than to predict the occurrence of an event that may harm it. Fragility can be measured; risk is not measurable (outside of casinos or the minds of people who call themselves “risk experts”). This provides a solution to what I’ve called the Black Swan problem—the impossibility of calculating the risks of consequential rare events and predicting their occurrence. Sensitivity to harm from volatility is tractable, more so than forecasting the event that would cause the harm. So we propose to stand our current approaches to prediction, prognostication, and risk management on their heads. In every domain or area of application, we propose rules for moving from the fragile toward the antifragile, through reduction of fragility or harnessing antifragility. And we can almost always detect antifragility (and fragility) using a simple test of asymmetry: anything that has more upside than downside from random events (or certain shocks) is anti- fragile; the reverse is fragile. * 

In the above snippet he references his earlier work on [Black Swans](http://www.amazon.com/The-Black-Swan-Improbable-Robustness/dp/081297381X/) and outlines the goal of antifragile entities is to withstand Black Swan events when they arise in the domain of the antifragile entity. The criteria as defined by the author for a Black Swan [wikipedia](http://en.wikipedia.org/wiki/Black_swan_theory#Identifying_a_black_swan_event):

    1. The event is a surprise (to the observer).
    2. The event has a major effect.
    3. After the first recorded instance of the event, it is rationalized by hindsight, 
    as if it could have been expected; that is, the relevant data were available but 
    unaccounted for in risk mitigation programs. The same is true for the personal 
    perception by individuals



## Antifragility and Software

With antifragility established as a goal to strive for, many developers who read Taleb's book started to float the idea of antifragile software, or software that becomes more powerful when chaos is applied to it, around.

Given how many people have struggled with fragile software, antifragile software seems like an amazing goal to have, but what would that actually look like? Can code actually become stronger when chaos and failures are hurled at it?

In Vikas Singh's blog post [Anti-fragile Software](http://scn.sap.com/community/abap/blog/2013/12/01/antifragile-software) he begins with the definitions for fragility, robustness, and antifragility, then proceeds to discuss how software for a long time has been stuck in the mindset of robustness being the end goal.

* Singh's definitions as mentioned above

  * Fragile : This is something that doesn’t like volatility. An example will be a package of wine glasses you’re sending to a friend.
  * Robust : This is the normal condition of most of the products we expect to work. It will include the wine glasses you’re sending to the friend, our bodies, computer systems.
  * Antifragile: These gain from volatility. It’s performance thrives when confronted with volatility.

> *Traditionally we have been designing software systems trying to make them robust and we expect them to work under all conditions.This is becoming more challenging as software is becoming much more complex and the number of components is increasing. *

Within a few paragraphs he then makes the following statement: 

> *We spend a great deal of effort in making a system robust but much in making it antifragile.The rough equivalent of antifragile is resilience in common language - it is an attribute of a system that enables it to deal with failure in a way that doesn’t cause the entire system to fail. *

Referring to the earlier definition from Taleb that Singh provided we see that antifragility MUST be beyond resilience, and as Singh's work continues, the only solutions brought forward simply increase resilience or robustness, not antifragility at all.
Singh's solutions that will be discussed later:

 * Create fault tolerant applications
 * Regularly induce failures to reduce uncertainty


## Finding Fragility

Let's start with a simple python example of a function:

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

Providing unit tests and more thorough documentation would help prevent a developer from checking an error like this into production as the test would fail, or they'd see the error of their thoughts before a keystroke was ever entered. That however is not antifragility, that's plain robustness. If code using this function was checked into the codebase with incorrect inputs that caused a failure, the code would not become stronger during the failure, it would simply fail. That is not antifragility at all, that is fragility, plain and simple.

## Robust Yet Fragile (RYF)

By deploying an application to a platform like [Amazon Web Services](http://aws.amazon.com/) the application gains the ability to "Sense, Scale, and Swarm" [Resilience p. 61](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431). Using monitoring services like [New Relic](http://newrelic.com/) the application developers can know when performance impacting conditions are occuring and these could be a simple traffic spike or a piece of infrastructure may have failed(Sense). 

Assuming the application has been designed to make use of distributed computer systems, it should be able to dynamically add new instances of the application to handle performance needs as they manifest(Scale). Swarming is the accomplished by the distributed units all coming together to continue the applications mission, whatever that may be(Swarm).

Even with an infrastructure that robust and dynamic, the application is still fundamentally fragile, a Black Swan event is just as likely to occur. After all a traffic spike is not a surprise nor does it have a major effect if the application was designed with the three S's in mind. A Black Swan for the application would could be some industry changing event like a new communications medium that is not supported.

These steps get us to Singh's goal of fault tolerant applications, but what about continually testing these faults? Continual testing such as Netflix's [Chaos Monkey](https://github.com/Netflix/SimianArmy) has certainly helped [Netflix](http://arstechnica.com/information-technology/2012/07/netflix-attacks-own-network-with-chaos-monkey-and-now-you-can-too/) to better serve its users, but again these are all from potentially known errors, none of them meet the 3 critical points to be a Black Swan and thus make a case for an Antifragile software entity.  

## Conclusion

Given the complexity from distrubted systems we are probably opening ourselves up to many more potential Black Swans. We are a the same time removing a ton of known issues and deploying software that is resilient to most of our known attackers, and given the dynamic nature of our industry that is probably the smart thing to do.

Rather than focusing on making software antifragile (Some form of intelligent AI that rewrites itself upon a stressor), we gain by creating simpler projects that properly handle a known set of conditions and address some need we as humans have identified.

This should be enough for developers to deal with, if a Black Swan occurs, a simpler path is to take what has been learned before and leverage that in the new environment. In this way, we may be antifragile, but there is no need to pretend our creations are. 

### Sources: 

##### Overview of Antifragile:

1. [Antifragile: Things That Gain from Disorder - Nassim Nicholas Taleb](http://www.amazon.com/Antifragile-Things-That-Gain-Disorder/dp/1400067820/ref=sr_1_1?ie=UTF8&qid=1388748417&sr=8-1&keywords=antifragile)

##### Overview of Resilience:

1. [Resilience: Why Things Bounce Back - Andrew Zolli & Ann Marie Healy](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431)

##### Advocates for Antifragile Software

1. [Anti-fragile Software - Vikas Singh](http://scn.sap.com/community/abap/blog/2013/12/01/antifragile-software)
2. [Agile is Antifragile - Stuart Wray](http://onfoodandcoding.blogspot.com/2013/05/agile-is-antifragile.html)
3. [Antifragile Systems: Designing for Agility vs. Stability - Mike Kavis](http://www.virtualizationpractice.com/antifragile-systems-designing-for-agility-vs-stability-22536/)

##### Criticisms of Antifragile (the book)

1. [Fragile Reasoning in Nassim Taleb’s Antifragile: An Enlightenment Transhumanist Critique - Gennady Stolyarov II](http://www.quebecoislibre.org/13/130515-8.html)
2. [Nassim Taleb Is Annoying, but Antifragile Is Still Worth Reading - John Horgan](http://blogs.scientificamerican.com/cross-check/2012/12/05/nassim-taleb-is-annoying-but-antifragile-is-still-worth-reading/)
3. [Anti-Fragile Book: Why We Should Eat Like Cavemen, Embrace Religion, and Hate Bankers - Marni Chan](http://www.policymic.com/articles/19909/anti-fragile-book-why-we-should-eat-like-cavemen-embrace-religion-and-hate-bankers)


