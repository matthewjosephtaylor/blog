---
layout: post
title: VSCode Is Awesome, Is Microsoft Giving Up On Being Evil?
date: '2017-04-02T22:58:49+00:00'
tags:
- vscode
tumblr_url: http://www.matthewjosephtaylor.com/post/159138628609/vscode-is-awesome-is-microsoft-giving-up-on-being
---
I’m typing this in VS Code.

A year or so ago I started using Atom as my light, friendly, small-footprint, general-purpose editor (for those times when using a heavy IDE like IntelliJ or Eclipse is too large a tool for the job).

I’ve enjoyed my time with Atom.  Like any useful tool there are some things I don’t like.

Written in coffeescript (A worthy language in its time but it lost, and I personally was never a fan)


Doesn’t handle large files well (neither does VS Code but it has the saving grace of refusing to open large files vs lagging-to-death or crashing, which is much preferred behavior) 
There are probably others but those are the ones I can think of off the top of my head, and really it is a pretty solid editor, and I wasn’t actively looking for a replacement.

Then comes an interesting new fact into my life, thanks to a lunch-discussion with a co-worker.

I learned that the source code for VS Code is under the MIT license



I knew that VS Code was licensed under an ‘open source’ license but there are OS licenses and there are OS licenses. I had assumed that Microsoft being Microsoft that they would have chosen an OS license that would would have allowed access to the source code but would have denied forking (you can see but you can’t touch). So I wrote it off as not being worth my time and attention.

I’m extremely picky on what I invest my time on. Rule of thumb: not 100% open = you have to pay me $$$ to spend time/attention on it. Closed source (including look but no touch licenses) is generally too big a risk unless there is a very large, obvious, and immediate payback.

The MIT license is well-known as perhaps the simplest, most permissive ''do what you will with the code’ license available. So this new information got my attention.

Life would be simpler if evil companies would just continue to do evil things. But alas, the world it seems is not that simple.

I’ve been playing around with VS Code for over the weekend, and so far it is doing everything that I have asked of it.

Key bindings are simple to remap (but perhaps a tad incomplete (no ''go back to last edit’ that I’ve been able to find so far)).
Every plugin I’ve wanted I’ve found, and they have been high-quality with recent development. The plugin ''marketplace’ is an active repository with a good rating system, and easy access to source repositories.
The ''project explorer’ is easily put away and recalled.
TypeScript is a language I’m actually excited to use. Long have I envied Lisp/Emacs user’s ability to easily reshape their editor at will. I had thought Atom would be the editor to scratch that itch, but I think I was just too turned off by coffeescript to make a go of it. Hopefully this will be the one…
The built in terminal is amazingly good. Like open vim in it and and it behaves well good. I can see myself living in this terminal.

Haha I just figured out that it appears to be using Apple Terminal under the hood. Well played.

Tasks are powerful but weakened significantly by being project-based. Hopefully this feature request will make it through.

In the meantime the macros plugin looks kind of cool, and it might just be a that a ''better tasks’ plugin already exists or might become my first plugin :)

VS Code Gotchas

There is no spell checker ''built in’.  No worries, there are plugins, but one of the top plugins is not to be trusted (sends all text to a 3rd party). There is now a warning message at the top of this plugin, but the fact that it exists at all, and got so popular is worrying
Complaints

The name ''Visual Studio Code’ 

Too similar a name to ''Visual Studio’ and ''Code’ too generic so it messes up google searches (I’m currently using ''vscode’ which seems to work fairly well)
The ''Visual Studio’ branding is not helpful for adoption among those of us who wrote off all things Microsoft long ago which I’m sure is hindering adoption (and I very much want the tools I use to be widely adopted to get as many network effect benefits as possible).

Everything requires a restart .

Reboots are not acceptable, there is no reason why things can’t be reloaded on the fly except poor programming practices.

WTF is this ’.vscode’ crap.

It is NOT COOL to litter up the filesystem with editor meta-data, especially without asking and making it clear this is going to happen.
Unintuitive that there are ''user settings’ which I’m guessing are the global settings and ''workspace settings’ which are tied to a project folder and seem to be responsible for creating the ’.vscode’ folder.  It creates a ’.vscode’ merely by ''looking at’ the ''workspace settings’ even if no changes are made.

Themes

There needs to be a theme explorer
Should be easier/possible for me to tweak theme properties

Still a little bit evil:

Telemetry/crash reporting on by default

How to turn it off

Has Microsoft really turned the corner?

I fully admit that I had written Microsoft off many years ago. The OS was crap. The company engaged in ethically unsound practices that garnered them a well-deserved reputation as an ''evil’ company. There was simply nothing about the company’s actions, or philosophy that lead me to believe they were worth any brain-cells, and so I intentionally stopped paying attention to them and avoided everything they produced.

I will stand by this decision to shun that despicable organization, and I think it has served me well over the years.

But recent actions such as releasing VS Code, TypesScript and I was amazed to learn in my lunch-time conversation dotNet including the CLR Under an MIT License, including a patent promise (which is better than nothing, but is still questionable…but really the whole idea software patents is questionable, so I’m going to leave that aside for the moment), strongly suggests that Microsoft is becoming worthy of attention once again. They are even making baby-steps into turning Windows into a decent OS by adopting compatibility with Linux of all things.

Actions do speak.

While I will forever remain wary. I am, for now, no longer going to auto-ignore everything coming out of Microsoft. They have earned a cautious, untrusting, eye…but an eye all the same. :)
