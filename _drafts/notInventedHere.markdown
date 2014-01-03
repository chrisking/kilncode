---
layout: post
title:  "Not Invented Here" or "How I Learned To Trust Again"
date:   2014-1-3
categories: software engineering, cognitive bias, new job
author: Matt Brown
---

What I learned about "Not Invented Here"

At my previous employer, we couldn't use anything that cost money. All of our monitoring, databases, infrastructure were all homespun (through a vareity of open source and self managed servers). If you brought up a hosted solution in front of my manger he would sneer and say something like "why would you pay someone else to do that." We had this mentality of penny pinching drilled into us so much that without realizing it I developed a bias against any piece of ops infrastructure that is not self hosted. You could call it "Not hosted here" bias. 

As part of the interview for my current job, I promised to add infrastructure and application performance monitoring to the platform to prepare for their impending launch to production. Once I joined the team, I set my estimate for two weeks to instrument the code, spin up some monitoring servers, automate the configuration of these servers, and do any other configuration required from  the hodgepodge of open source tools I had planned to use for the task (shout out to [graphite](http://graphite.wikidot.com/)). The CTO told me "Yeah, that's cool, but before you start implementing all that, I want you to try out a hosted solution." Internally I balked, "But, those cost a money!" and "They are going to have data about our app!". For the next couple of days I tried various hosted solutions while internally fighting with the part of me that sneered at hosted solutions. I was not prepared for how EASY it all was. Not only was it easy and relatively cheap, it was was cheap enough that I would pay the cost out of pocket just to not have to manage the tools myself, I could instantly see the time I would save both in configuration and upkeep. 

Our CTO wasn't blinded by Not Invented Here. He knew that it'd be a much better use of time to work on actual issues with the app than to build a castle of monitoring solutions. Suddenly free from all of that work, we now have several extra weeks to run load tests and make improvements we otherwise wouldn't have had time to make before launch. By properly avoiding the bias of "Not Invented Here" we are able to focus on the code that is unique and important to our business and not get distracted by castle building. 

How often are you looking at some software for sale or some open source project that isn't doing exactly what you want and you think to yourself "I could do this better." As software engineers, we have the skill and ability to design and write any number the of complicated systems that we deal with day to day. We know the "best way" to do this or that and figure it'll take no time at all to write our own DB, develop our own monitoring system, or make a prettier javascript library. This attitude is what makes software engineers great and open source software so popular. But "I could do this better" can transform into a disease of only wanting to use things you've made. This happnes in organizations all the time and is called "Not Invented Here." It's a management bias against any type of software that isn't made in shop. Your company gets into this mindset of trusting no one but themselves "cause we're smart." 
What this ends up looking like is a team taking on too much work. You lower your profit margin by having to support more code and support the construction of new code for the pieces that grow as your company does. And this doesn't just affect the code product that you're writing, it can also become a problem in your infrastructure. Often companies will refuse to use products such as AWS or New Relic because they are worried about their data or "getting attached to one system" or having to pay money for a service they could do for free. The problem with these arguements is that time is an engineer's most precious resource. The only way to make efficient use of time is to be really good at fortune telling. The further something is into the future, the less accurate your estimates are going to be. The less you know about how an application works, the worst your estimates are going to be. Side note: this is what makes agile work so well, shorten the feedback loop between when you get requirements from a user and when you show it to them so that you can make better estimates. Once you realize the value of your engineers' time then you can start to make educated decisions about whether to build something yourself or to outsource it. You are in a business to make money doing something, it makes sense if as much of your business as possible is focused on that core competancy. 
I've run into this recently with my new job. 



Not invented here as a bias
How it affects an organization
Talk about time as a resource
Using more open source
Thinking about this as a way to better manage your personal time
