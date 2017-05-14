---
layout: post
title: "My Own Private Low Power Server(s)"
date: 2017-04-16T19:01:42-05:00
categories: server awesome
published: true
---

# It Is 2017

[Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law) is both dead and alive.

It is dead because personal computers are not getting any faster processors. We've reached the physics wall with regards to how fast we can make a single processor go without melting it.

![CPU's not getting faster](https://web.archive.org/web/20170417003750/https://www.extremetech.com/wp-content/uploads/2012/02/CPU-Scaling.jpg)

It is alive because the transistor counts are continuing to rise nicely.

So what does this mean?

It means that instead of going tall (one big server/application to run everything) we are all being encouraged to go wide (many little services doing simpler and simper tasks).

It also means things like [functional programming](https://en.wikipedia.org/wiki/Functional_programming) will eventually rule the world (but that is a story for another time).

I have to ask how does this trend effect me personally with regards to my consumption of computing resources? 

On the home front, I'm close to the point where I no longer wish to build and maintain my own hardware. There are a plethora of services now that allow one to quickly, easily, and cheaply get their hands on as much or little computing power as they could desire.

Yet I don't think we are quite at the point where I can entirely rely on 'The Cloud' for all my computing needs. 
- It's not quite fast and cheap enough (it's darn close though). I have and will continue to take more and more advantage of online cloud service providers where it makes sense to do so, but for high-bandwidth network traffic in particular it just doesn't seem to add up.
- I have security concerns
	- Not fast and easy as it needs to be to synchronize storage and compute fall-over between providers. I don't want a single companies death to lead to my inability to access my data and services.
	- Privacy concerns (the real sticking point). I encrypt my data, all of it. I don't want an enterprising hacker, shadowy organization, or random person, to have access to my private thoughts. I'm at a point in my life where the computing resources I use have become an [extension of my brain](https://en.wikipedia.org/wiki/Exocortex), and so just like I take my mental privacy seriously, I take my personal computing privacy seriously. 
	Encryption isn't a perfect solution due to the fact that the computer can only deal with the information in clear text.  So there is always in running memory a key that can unlock everything. Running encryption on a cloud-farm server pre-supposes absolute trust of the service provider, since it would be trivial for them to gain access to that key (or a hacker, who hacked the service provider, etc...). The only reason I trust it for my home server is necessity + my ability to control the physical hardware. Perhaps a breakthrough in [Homomorphic Encryption](https://en.wikipedia.org/wiki/Homomorphic_encryption) will solve this personal dilemma, but unfortunately it isn't here yet.

There is also an undeniable joy for me in building. I like making things. :)

So in 2017, if one goes about building a personal computing environment what should it look like?

What are my own particular needs?
- Reliable
- Expandable
- Cost-efficient

With these goals in mind, and after hours of research on [newegg](https://www.newegg.com/) and [cpubenchmark](https://www.cpubenchmark.net/) I crafted my plan.

1. I needed to get my hands on as many _cores_ as cheaply as possible rather than chasing _ghz_.
2. If you scale down the _ghz_ by a factor of 2x you can scale down the power by a factor of 10x which leads to...
3. Lower Watts which drives down running costs, and heat which leads to....
4. Passive cooling which reduces noise, increases reliability, and lowers maintenance hassles. 

At a certain point it just clicked that I was looking to build the cheapest, lowest-watt _set_ of servers possible.

My plan is to start with 3 to get the benefits of redundancy, and then add more as time goes on.

The configuration I've chosen looks like:

| Part          | Name          | Price |
| ------------- |---------------| ----- |
| Motherboard + CPU | [ASRock J3160DC-ITX](https://www.newegg.com/Product/Product.aspx?Item=N82E16813157714) / [Celeron J3160](http://www.cpubenchmark.net/cpu.php?cpu=Intel+Celeron+J3160+%40+1.60GHz) | $105 |
| Memory | [16GB DDR3 1600](http://amzn.to/2nTdt1C) | $90 |
| OS Drive | [2.5" 16GB SSD](http://amzn.to/2nTe978) | $21 |
| Storage Drive | [3.5" 8TB (some disassembly required)](http://amzn.to/2p8P7B9) | $208 |
| Case | [Mini-ITX](http://amzn.to/2prU592) | $40 |
| **Total**||**$464**|

Note that the motherboard _also_ includes a power-supply that comes in the form of a power-brick (further reducing costs, and noise, etc..., one can sense a trend.).

I admit that I splurged on the size of the storage drive, and the amount of ram (old habits die hard). One could easily get away with halving one or both of those to get the cost closer to $300.

I looked closely at both [Intel's NUC](http://amzn.to/2ol9SEw) and [Zotac's C-Series](http://amzn.to/2pH6LYW). The deal-breaker there was mostly around the $/TB of storage since both go with a 2.5" form factor, and for the moment the 3.5" spinning platters are still king (~$100 for 2TB vs ~$200 for 8TB, a 2x difference is just hard to swallow).

## What the final product looks like:
![It begins](https://c1.staticflickr.com/5/4187/34636436865_f124006a9b_z.jpg)

![Finished](https://c1.staticflickr.com/5/4171/34636433565_b51a7cc5a6_z.jpg)

![It's Alive](https://c1.staticflickr.com/5/4183/34250839680_9179d3b51c_z.jpg)