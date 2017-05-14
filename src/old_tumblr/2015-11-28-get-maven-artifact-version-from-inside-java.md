---
layout: post
title: Get Maven Artifact Version from Inside Java Runtime
date: '2015-11-28T13:00:20+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/134139198434/get-maven-artifact-version-from-inside-java
---
Simple static method to get maven artifact version.

I was doing some build magic to get this info, but maven gives the pom.properties file for free, so why not take advantage of it?

Important that the class that is passed in is contained within the maven artifact (jar file).

{% highlight javascript %}
    Properties properties = new Properties();
    try {
        InputStream is = clazz
                .getResourceAsStream("/META-INF/maven/" + groupId + "/" + artifactId + "/pom.properties");
        if (is != null) {
            properties.load(is);
        }
    } catch (IOException e) {
        throw new RuntimeException(e);
    }
{% endhighlight %}
}
