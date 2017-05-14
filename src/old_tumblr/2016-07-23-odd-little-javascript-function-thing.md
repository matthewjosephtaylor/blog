---
layout: post
title: Odd little javascript function thing
date: '2016-07-23T13:08:55+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/147854627799/odd-little-javascript-function-thing
---
I’ve been playing a lot of screeps, which means I’m getting back into doing more serious javascript.

It’s been a few years since I last did anything big with javascript ( example ) and it is nice to see that there have been a series of improvements made to the language.

‘let’ is my favorite new addition so far.

By accident I discovered that this works:

let obj = { doAThing() { console.log(''wtf?'');}}
obj.doAthing(); // returns ''wtf?''


But oddly this does not work:

doAThing() { console.log(''wtf?''); }
// Uncaught SyntaxError: Unexpected token {


Doing a bit of googling around I can’t seem to find where this new function definition mechanism was introduced, which I find odd because it is really nice.

It stops me from having to write code like this:

ojb = { doAThing: funciton doAthing() {...} }


I like to write the above code as it both names the function and gives it an object property name.  Function names are nice because it allows one to include those function names in logs.

I’m reticent to use this newly discovered function definition syntax as I can’t see anywhere that it is defined as legal (is it new, has it been around since forever?). I’m also bothered by the inconsistency, which makes me think that this syntax works ''by some weird accident’ that I don’t fully understand (though it is too useful not to be intentional). I’ll update as I discover more about this odd/cool little ''quirk’ of the language I’ve discovered, that has amused me so.
