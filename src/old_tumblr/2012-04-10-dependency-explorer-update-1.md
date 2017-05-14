---
layout: post
title: 'Dependency Explorer Update #1'
date: '2012-04-10T01:46:10+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/20831884138/dependency-explorer-update-1
---
One of my friends discovered a set of maven repository mirrors.
[http://docs.codehaus.org/display/MAVENUSER/Mirrors+Repositories
](http://docs.codehaus.org/display/MAVENUSER/Mirrors+Repositories)

Ibiblio FTW!
```
rsync -a -v –include “*/” –include “*.pom” –include “*.xml” –exclude “*” –bwlimit=1000 mirrors.ibiblio.org::maven2/ maven2
```
The above gets the complete set of pom files and xml metatdata files for the entire maven central repository.

Plan on getting the rest of the artifacts via a ‘slow slurp’ to not put too much pressure on ibiblio’s servers.  It will probably be weeks before I’m ready for the full dataset anyway so no rush.
