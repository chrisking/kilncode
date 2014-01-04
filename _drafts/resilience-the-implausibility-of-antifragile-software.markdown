---
layout: post
title:  "Resilience, The Implausibility of Antifragile Software"
date:   2013-12-31 18:59:03
categories: software engineering, systems theory
author: Chris King
---

### What is Antifragile?

Nassim Nicholas Taleb defines antifragile in his book "Antifragile" as: "beyond resilience or robustness. The resilient resists shocks and stays the same; the antifragile gets better." [excerpt here](http://www.fooledbyrandomness.com/prologue.pdf) The examples provided for antifragile entities include media pundits, whose reputations don't depend on being correct, and muscles, as they rebound to be even stronger than they were before the stressor was applied.

### Antifragility and Software

With antifragility established as a goal to strive for, many developers who read the text started to float the idea of antifragile software, or software that becomes more powerful when chaos is applied to it, around.

Given how many people have struggled with fragile software, antifragile software seems like an amazing goal to have, but what would that actually look like? Can code actually become stronger when chaos and failures are hurled at it?

In Singh's (add first name) blog post [Anti-fragile Software](http://scn.sap.com/community/abap/blog/2013/12/01/antifragile-software) he begins with the definitions for fragility, robustness, and antifragility, then proceeds to discuss how software for a long time has been stuck in the mindset of robustness being the end goal.

> *Traditionally we have been designing software systems trying to make them robust and we expect them to work under all conditions.This is becoming more challenging as software is becoming much more complex and the number of components is increasing. *

Within a few paragraphs he then makes  the following statement: 

> *We spend a great deal of effort in making a system robust but much in making it antifragile.The rough equivalent of antifragile is resilience in common language - it is an attribute of a system that enables it to deal with failure in a way that doesn’t cause the entire system to fail. *

Referring to the earlier definition from Taleb we see that antifragility MUST be beyond simple resilience, and as Singh's work continues, the only solutions brought forward simply increase resilience or robustness, not antifragility at all. 


### Finding Fragility

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

### Robust Yet Fragile (RYF)



#### Notes:

Nassim Nicholas Taleb wrote Antifragile, a book advocating we ourselves become antifragile, or that we become better trhough chaos and disorder around us.

Many have claimed that we have the ability to build software that itself is antifragile, including such techniques as continuous integration, 0 downtime migrations, and elaborate failover mechanisms. 

In this post I will argue that these endeavors, while they certainly improve software for all parties, they in no way create antifragile software. Additionally I will argue the best we can hope for is resilience or robustness in our codebases, and that is OK.


#### Sources: 

##### Overview of Antifragile:

1. [Antifragile: Things That Gain from Disorder - Nassim Nicholas Taleb](http://www.amazon.com/Antifragile-Things-That-Gain-Disorder/dp/1400067820/ref=sr_1_1?ie=UTF8&qid=1388748417&sr=8-1&keywords=antifragile)

##### Overview of Resilience:

1. [Resilience: Why Things Bounce Back - Andrew Zolli & Ann Marie Healy](http://www.amazon.com/Resilience-Why-Things-Bounce-Back/dp/1451683812/ref=tmm_pap_swatch_0?_encoding=UTF8&sr=8-1&qid=1388748431)

##### Advocates for Antifragile Software

1. (http://odetocode.com/blogs/scott/archive/2013/06/21/antifragile-software.aspx)
    * Probably going to be removed as a source, the document here highlights the incorrect idea of antifragile with Netflix's Chaos Monkey project, but doesn't delve into many details.
2. (http://scn.sap.com/community/abap/blog/2013/12/01/antifragile-software)
3. (http://onfoodandcoding.blogspot.com/2013/05/agile-is-antifragile.html)
4. (http://www.virtualizationpractice.com/antifragile-systems-designing-for-agility-vs-stability-22536/)

##### Criticisms of Antifragile (the book)

1. (http://www.quebecoislibre.org/13/130515-8.html)
2. (http://blogs.scientificamerican.com/cross-check/2012/12/05/nassim-taleb-is-annoying-but-antifragile-is-still-worth-reading/)
3. (http://www.policymic.com/articles/19909/anti-fragile-book-why-we-should-eat-like-cavemen-embrace-religion-and-hate-bankers)


