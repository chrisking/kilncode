---
layout: post
title:  "Not Invented Here"
date:   2014-1-6 18:59:03
categories: 
author: Matt Brown
---



The past few weeks I've been thinking a lot about the "Not Invented Here" bias where a person subconsciously avoid innovations not created by them or their organization. The reasons stated for the bias can vary from cost motivations to fear of something you didn't write yourself. Recently I discovered myself employing this bias and learned to overcome it. 

At my previous employer, we couldn't use anything that cost money. All of our monitoring, databases, and infrastructure were homespun (through a variety of open source and self-managed servers). If a hosted solution were brought to my manager, he would sneer and say something like, "Why would you pay someone else to do that." We had this mentality of penny pinching drilled into us so much that, without realizing it, I developed a bias against any piece of ops infrastructure that is not self-hosted. I consider this a subset of “Not Invented Here” called "Not Hosted Here" bias. 

As part of the interview for my current job, I promised to add infrastructure and application performance monitoring to the platform to prepare for their impending launch to production. Once I joined the team, I set my estimate for two weeks to instrument the code, spin up some monitoring servers, automate the configuration of these servers, and do any other configuration required from the hodgepodge of open source tools I had planned to use for the task (shout out to [graphite](http://graphite.wikidot.com/)). 

The CTO told me "Yeah, that's cool, but before you start implementing all that, I want you to try out a hosted solution." 

Internally I balked. "But, those cost money! They are going to have data about our app!" 

For the next couple of days I tried various hosted solutions for monitoring while fighting with the part of me trained to sneer at paying other people to do this. 

I was not prepared for how EASY it all was. 

Not only was it easy and relatively cheap (cheap enough that I would pay the cost out of pocket just to not have to manage the tools myself), I could instantly see the time I would save both in configuration and upkeep. 

Our CTO wasn't blinded by "Not Invented Here". He knew that it'd be a much better use of time to work on actual issues with the app than to build a castle of monitoring solutions. Suddenly free from all of that work, we now have several extra weeks to run load tests and make improvements we otherwise wouldn't have had time to make before launch. By properly taking into account the bias of "Not Invented Here", we are able to focus on the code that is unique and important to our business and not get distracted by problems other people have solved. 

I don't want to give the impression that I think all monitoring information should be outsourced. "Not Invented Here" was a bias that was subconciously affecting the way that I was making important infrastructure decisions. Now that I am aware of my decision making preference towards avoiding other people's software, I can make smarter and more informed decisions.
