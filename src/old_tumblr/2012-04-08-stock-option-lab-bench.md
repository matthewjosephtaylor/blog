---
layout: post
title: Stock Option Lab Bench
date: '2012-04-08T13:25:02+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/20725314416/stock-option-lab-bench
---
I’d like to start investing more in stock options, but I want to play with a great deal of what-if scenarios before I commit any of my hard-earned cash.  I want to learn and get a feel for how stock options work ‘in the real world’, not idealized mathematical models.

So I’m going to create a database (MongoDB most likely), load it with tons of historical stock option data (and maybe other interesting time-series data), and create some software that allows me to efficiently test strategies in an automated fashion.

I’ve played with genetic algorithms and neural networks in the past, however the downside to using those is that one is unable to understand what makes the final strategy tick.  The upside of course is that one can use the power of the computer to adaptively explore the data for good strategies, so I definitely want to use them, but need to tame them.  So I’m thinking this time I’ll concentrate on extremely simple GEs/NNs (Learners), and preprogram a small collection of strategies that the Learner can combine to use.  This limits the possible strategies severely, but really I want this system to teach ME what strategies work, and I being a mere human, I can only comprehend relatively simple stories.

Lots of data, and lots of calculations.  I need to write the software/dataset such that it can scale, and I can take advantage of things like Amazon’s EC2.  To my mind this means heavy reliance on functional programming.  Ideally it would probably be best to use a language like Erlang, or Scala.  I’m going to start in Java though, simply because that is the language I already know, and I know I can get results quickly.  I’ll attempt to use a functional style wherever possible, and may switch to another language if I have difficulties making Java perform.
