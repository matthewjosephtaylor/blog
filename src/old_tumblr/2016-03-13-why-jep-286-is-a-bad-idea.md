---
layout: post
title: Why JEP 286 is a Bad Idea
date: '2016-03-13T12:44:30+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/140979159999/why-jep-286-is-a-bad-idea
---
Recently there has been a bit of talk about adding ‘var’ as a keyword to shortcut some of the ceremony around local variable instantiation.

This is so this:

List<String> stringList = new ArrayList<String>();


becomes this:

var stringList = new ArrayList<String>();


The full JEP is here:

http://openjdk.java.net/jeps/286

I’m in the negative camp.  Here is why:

I like seeing the type on the left hand side so I can instantly discern the type rather than having to go to the method definition to find out.

var whatTypeAmI = foo.zoinc();


I don’t want to spend extra thought-cycles trying to imagine or look up, or remember what the type is. When I’m reading code I want to instantly at a glance know what the type is.

Also, since there is no way to specify an interface, the var will necessarily have to be typed the same the full class.

// typed to ArrayList instead of List
var num = new ArrayList();


This makes it difficult to ''code to the interface’. It is generally better to constrain the type to a narrower interface whenever possible. Use of var leads away from this core principle.

The counter argument will of course be that one isn’t forced to use the new var keyword, and that it should be a ''best practice’ not to use it in such instances. To which I would argue that programmers are lazy and will almost always prefer the easier path. If var exists it will be used relentlessly, whether it is ''correct’ or not.

All in all I think this is a poor direction for Java to go. It is an attempt to round off some of the rough edges, but sometimes rough edges are more useful than they are annoying.

Would you rather deal with sharply cornered bolt heads or a rounded off ones, when you are tasked with disassembling an engine?
