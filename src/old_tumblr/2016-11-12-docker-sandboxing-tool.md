---
layout: post
title: Docker Sandboxing Tool
date: '2016-11-12T18:34:16+00:00'
tags:
- docker shell script
tumblr_url: http://www.matthewjosephtaylor.com/post/153102827644/docker-sandboxing-tool
---
Well I just spent my entire Saturday writing a tool for quickly and easily creating sandboxes in docker.

This has been something that I’ve wanted for a while and although I hadn’t intended to devote this much time to it today…it was one of those things where I couldn’t stop myself until I finished it. :)

I think I ended up creating kind of a neat tool.

https://github.com/matthewjosephtaylor/docksand

The basic premis is that the work-dir is on the host machine, and all the OS stuff is inside a docker container.

This is effectively just a nice shell script for those times when you want to do something like docker run -it --rm --entrypoint=/bin/bash image-name but want to  preserve the container, mount host volumes and re-use the container.
