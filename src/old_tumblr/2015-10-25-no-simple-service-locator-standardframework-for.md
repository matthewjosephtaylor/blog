---
layout: post
title: No Simple Service Locator Standard/Framework for Java?
date: '2015-10-25T14:45:36+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/131898779419/no-simple-service-locator-standardframework-for
---
I want to do a simple, but critical thing in Java and I’m not having a great deal of luck in finding examples of other people doing this.

What I want is a simple and hopefully standard pattern/framework/library that will let me easily locate Service Objects that I don’t plan on exposing outside of a program.

When people think SOA (Service Oriented Architecture) they immediately start thinking about networks and things like REST and WSDLs and SOAP. However, it seems that in the rush to expose services not much has been written about best practices or standards for services that are internal to a program and are explicitely not exposed.

Non-network exposed services are important too!

Martin Fowler wrote a nice article in 2004 explaining the various pros and cons of using service locators vs dependancy injection. This guy wrote an updated article in 2012 that is based on Fowler’s article and gives more-or-less the state of play in the Java world today.

TLDR; Spring came along and dependancy injection sort of won the hearts and minds battle.

Fowler’s words on the critical difference between Dependancy Injection and Service Locators:


  The important difference between the two patterns is about how that implementation is provided to the application class. With service locator the application class asks for it explicitly by a message to the locator. With injection there is no explicit request, the service appears in the application class - hence the inversion of control.


A problem I have with DI (especially the annotation driven form of DI) is that it makes debugging more of a pain, that it puts a bit of magic between the developer and the runtime code.

The developer is also forced to use, understand, and cofigure a somewhat conceptually heavy framework like Spring or Guice before they can even really start coding.

I haven’t played with Guice, but I know that Spring slows down program start as it scans for annotations and does its DI autowire magic. This is bad as it slows down the flow of the edit/compile/run devlopment loop.

But the main problem for me with both frameworks is lack of control I as a developer have. As a developer I want to know exactly what is happening in the lifecycle of an object, and how one object comes to know about another object. And I want to be able to discover this information by reading the code, not by reading documentation on the framework on how it conceptually works.

Anyway enough ranting on why I don’t particluarly like DI.

Fowler’s words on why one perhaps wouldn’t want to use a service locator:


  The key difference is that with a Service Locator every user of a service has a dependency to the locator. The locator can hide dependencies to other implementations, but you do need to see the locator. So the decision between locator and injector depends on whether that dependency is a problem.


To my mind this isn’t actually a ‘real’ problem. This problem is caused by a lack of a standard. There should be a JSR concerning service location (and no JNDI doesn’t count). There needs to be something like JSR 330 but for Service Locators. Maybe it exists and google is failing me but if it exists I haven’t found it.

But that is almost beside the point.

The real real problem with both Dependancy Injection and Service Location is how to assemble stuff. How does Object A know about Service B, and how does Service B get instantiated?

With DI and JSR 330 assembly is left to the magic of the framework.

That is a huge failing as that is the important part.

Ah, but I hear you say what about OSGi?

Perhaps maybe that is the ultimate answer, but OSGi is really more about modular components than Service Location. It also comes with even more conceptual overhead and a runtime setup. If there was a standard for Service Location in java then this would probably be it. But it is a bigger monster than I want and need to have to deal with.

There is also Project Jigsaw

This has the distince disadvantage of not existing yet. From what I’m reading about it, it is Oracle’s attempt to bring OSGi into the mainstream and is mostly concerned with building modules not services.

Alas, there just doesn’t seem to be anything in existence that does what I want.  So I’ve gone to the trouble to write my own. I don’t like this. This is the sort of thing one uses someone else’s framework or library for.  But in 2015, after 20 years of development it seems that there is not a standard mechanism for doing this very basic, very simple thing.

```
public class ServiceLocator {

    @Override
    protected Map, Object> initialValue() {



    @SuppressWarnings("unchecked")
    final T object = (T) services.get(clazz);
    if (object == null) {
        throw new RuntimeException("Unable to locate service for class: " + clazz.getCanonicalName());
    }
    return object;

    @SuppressWarnings("unchecked")
    final T object = (T) threadLocalServices.get().get(clazz);
    if (object == null) {
        throw new RuntimeException("Unable to locate service for class: " + clazz.getCanonicalName());
    }
    return object;

    services.put(clazz, serviceImpl);

    services.remove(clazz);

    threadLocalServices.get().put(clazz, serviceImpl);

    threadLocalServices.get().remove(clazz);

}
```

I don’t claim this is perfect, and it doesn’t solve the hard part of assembling the services.  But it does allow one to write code like this:


```
@Produces(MediaType.APPLICATION_JSON)
public Iterable listAccounts() {
    return ServiceLocator.get(AccountService.class).getAccounts();
```


Addendum

After a bit more research and stumbling around I discovered to my amazement that there is a native java mechanism for Service Location: ''ServiceLoader’ but nobody uses it (and I don’t blame them).

Here is an IBM develperworks article appropriately titled ''5 things you didn’t know about … everyday Java tools’ that explains it a bit.

Long story short It is pretty close to what I want, but it’s clunky and uses files in META-INF to grab implementation classes.

Then I discovered that netbeans has a ''Lookup’ utility class that is a wrapper around ServiceLoader that people point to as a possibility but it seems to have the same issues that ServiceLoader does.

In the end like I said before it is the assembly part that is the hard part.  I don’t consider putting specially named text files with class names in them to be acceptable.

Wiring and implementation loading IMHO shouldn’t be a configuration detail (either via text/xml files or annotation scanning). That needs to be a Java compiler screams at you if you get it wrong sort of thing, and so needs to live in Java code land. Text/XML config files for this sort of thing was an experiment that was tried, and failed miserably, and now we’ve learned the lesson and need to move on.

If I come up with what I think of as a decent Service Assembly Pattern I’ll post it. For now I just have a class that looks like this:

```
public class ServiceAssembler {

    ServiceLocator.register(AccountService.class, new AccountServiceImpl());
}
```
