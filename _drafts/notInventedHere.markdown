---
layout: post
title:  "Not Hosted Here"
date:   2014-1-3 18:59:03
categories: software engineering, cognitive bias, new job
author: Matt Brown
---

### Not Invented Here

Over the past few weeks I have been thinking a lot about the "Not Invented Here" bias, or when one subconsciously avoids innovations not created by oneself or one's group. The reasons stated for the "Not Invented Here" bias can vary from cost motivations to fear of something not written by oneself. Recently, I discovered myself employing this bias and learned to overcome it. 

At my last place of employment, we could not use anything that cost money. All of our monitoring, databases, and infrastructure were homespun through a variety of open source and self managed servers. If an employee brought up a hosted solution in front of the manager, the manager would sneer and say something like, "Why would you pay someone else to do that?" My coworkers and I had the penny-pinching mentality drilled into us so often that I subconsciously developed a bias against any piece of ops infrastructure that was not self-hosted. One could call it "Not hosted here" bias. 

As part of the interview for my current job, I promised to add infrastructure and application performance monitoring to the platform in order to prepare for their impending launch to production. Once I joined the team, I set my estimate for two weeks to instrument the code, spin up some monitoring servers, automate the configuration of these servers, and do any other configuration required from the hodgepodge of open source tools I had planned to use for the task (shout out to [graphite](http://graphite.wikidot.com/)). 

The CTO told me, "Yeah, that's cool, but before you start implementing all that, I want you to try out a hosted solution." 

Internally I balked, "But, those cost money!" and "They are going to have data about our app!". 

For the next couple of days I tried various hosted solutions for monitoring while fighting with the part of me trained to sneer at paying other people money to do this. 

I was not prepared for how EASY it all was. 

Not only was it easy and relatively cheap (it was was cheap enough that I would pay the cost out of pocket just to not have to manage the tools myself), but I could instantly see the time I would save both in configuration and upkeep. 

Our CTO was not blinded by "Not Invented Here". He knew that it would be a much better use of time to work on actual issues with the app than to build a castle of monitoring solutions. Suddenly free from all of that work, we now have several extra weeks to run load tests and make improvements we otherwise would not have had time to make before launch. By properly taking into account the bias of "Not Invented Here", we are able to focus on the code that is unique and important to our business and not get distracted by problems other people have already solved. 