---
layout: post
title: Vaadin/GWT and Maven annoyances
date: '2013-05-08T16:39:52+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/49960070610/vaadingwt-and-maven-annoyances
---
I love Vaadin but it is a bit broken in regards to how it deals with maven.
Maven is a beast, but if one is doing any form of serious java development it is really the only game in town. There is really no excuse if your doing any serious Java development for not using maven.
Vaadin actually has good support for maven except for one major annoyance: by default the Vaadin archetype places the gwt generated javascript inside of src/main/webapp/VAADIN by default.
There is a convention for where to place generated sources for maven projects: target/generated-sources
Unfortunately generating this javascript takes a long time and only needs to be done when a gwt widget is added/modified. Thus the hack of depositing the generated javascript inside of src/main instead of target.Maybe having the archetype behave this way is OK because it gets the project up and running quickly, but it is definitely a bad practice IMHO.
Personally I’m looking at just creating a separate maven module to deal with the generated javascript. It will probably be a bit of a pain to get maven happy with including javascript outside of the module for the war file, but there really doesn’t appear to be a cleaner solution.For the moment I’ve simply created a new ‘generated’ directory at the top of my maven root directory and am dumping the javascript there. It is still a hack, but I feel it is a significantly cleaner hack.
