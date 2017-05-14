---
layout: post
title: Maven All-in-one (single jarfile) application archetype
date: '2012-04-21T18:11:02+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/21530531195/maven-all-in-one-single-jarfile-application
---
I’ve created a maven archetype that creates an all-in-one (single jarfile) application complete with application-runtime access to build-number and maven artifact version.https://github.com/matthewjosephtaylor/application-archetypeI’m jumping through the hoops now to get this published to the maven central repo (which is an interesting process all on its own).  Looks like the only way to get it done is to use Sonatype OSS repository which is acting as a sort of gatekeeper.  Why on earth isn’t github an “Approved Hosting Location”?

Helpful resources for creating an maven archetype and publishing to maven central repository:
http://johnjianfang.blogspot.com/2009/05/create-maven-archetype-from-existing.html
http://maven.apache.org/guides/mini/guide-central-repository-upload.html
https://docs.sonatype.org/display/Repository/Choosing+your+Coordinates
https://docs.sonatype.org/display/Repository/Sonatype+OSS+Maven+Repository+Usage+Guide
