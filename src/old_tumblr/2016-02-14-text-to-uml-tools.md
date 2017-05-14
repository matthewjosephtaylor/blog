---
layout: post
title: Text to UML Tools
date: '2016-02-14T13:10:38+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/139307697304/text-to-uml-tools
---
I’m sick of using a mouse to do diagrams.

I’m a coder.  I want to write some code and have a pretty diagram pop out the other end.

Googling around a bit, this appears to be the best list of current text to UML tools:

http://modeling-languages.com/uml-tools/

After looking at all of them, this is my favorite as far as ease of use and quality of the diagram produced:

https://github.com/skanaar/nomnoml

Written in javascript. Can just clone the repo, do npm install, open the index.html in your favorite browser and go.

Also an online version for the lazy and to test it out:

http://nomnoml.com/

I love the syntax, the diagrams look good, easy to use out of box, and after looking at the code, easy to understand how it works.



Unfortunatley, it really only does class diagrams (which can kind of forced to be block diagrams as well), and the ‘stereotypes’ that are baked in are a bit limited.

I’ve devoted a bit of time to extending the stereotypes, and discovered I suck at html5 canvas 2d drawing. So creating stereotypes by hand isn’t going to happen, at least not easily. Plus I really, really want an interaction diagram as well.

Next new favorite I’ve discoverd is:

http://plantuml.com/

An online version is here:

http://www.planttext.com/planttext

A complete set of diagrams.  The syntax is clean. As far as functionality goes this one has everything.

There is only one problem: The diagrams are IMHO ugly.



Under the hood plantuml appears to be creating dot files that it feeds into graphviz.

Dot it turns out is kind of a neat language.

A very neat language.

Dot itself was probably what I was looking for when I began my adventure, but plantuml on top of dot is where I would have ended up anyway since it adds the UML specific syntax.

I now have more or less what I wanted. I’m just a tad unhappy that the results are a bit rougher than I would like. Story of my life. :)

Now I just need to figure out a way to make dot graphs pretty.

Edit:

I bit the bullet and created a ''skinparam’ style file that can be included so the graphs don’t look quite so ugly.

https://github.com/matthewjosephtaylor/plantuml-style

(incidently, the fact that the plantuml language has local and url includes and macros is powerful…and dangerous :) )
