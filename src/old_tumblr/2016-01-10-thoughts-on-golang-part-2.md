---
layout: post
title: Thoughts on Golang (Part 2)
date: '2016-01-10T14:59:46+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/137038574614/thoughts-on-golang-part-2
---
Continuing from part one

interfaces: Feels a bit like duck typing. Very flexible. Allows one to create interfaces for already existing types which is neat. Puts more of the onus on the user of the interface vs the creator of the type, which feels a bit backwards. In effect the method signature becomes the interface. Loses some of the ‘contractyness’ of the concept in exchange for putting the module user more in control.
The case statement is finally useful! By getting rid of the disastrous automatic fallthrough which is how it behaved in C (and therefore many other languages) one can actually use a case statement and have it do what you think it should do, and therefore it becomes a useful language feature vs a vile pit of bugs. Aweseome!
type assertions: The syntax is a bit odd, but it works.  Thanks to the sane way that case statements work, and the fact that one can switch on the type assertion, doing ''type switching’ becomes a very elegant way of dealing with an unknown type. A+
go routines: Feels weird that one doesn’t get a handle to the thread. In general one shouldn’t need such a handle but they are nice to have at times. Perhaps there is a way to get the handles, or get a more detailed view of the runtime of the running threads I’ll run into later. Bye bye thread local storage.
channels: Weird that the <- does double duty for both sending and receiving.
Panic feels very much like an exception without the ability to type the exception. Exception types often are not so helpful, so one could see it as a useful simplification. One can even simulate exception handling via use of panics and deferred resolves. I’m beginning to suspect that panic might be the cleaner way to do error handling. Just a bit odd that the ''catch’ has to be at the top. Actually I think I kind of like that better anyway.
// something like a Java try/catch in go
{% highlight python %}
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("recovered")
        }
    }()
    fmt.Println("step 1 will be called")
    funcThatPanics("help I need an adult!")
    fmt.Println("step 2 will never be called")
}()
{% endhighlight %}

Can use range on channels. Nice.
Use of <-x vs x<- to determine reader/writer is cute. Still think <- should be split into two operators. Would make this less cute, but more expressive.
The len() function feels very lispy to me for some reason. I guess because it is the primitive operation for determining the length of ''something’.
New phrase: ''goroutine leak’. When a goroutine is blocked waiting on a channel that will never be be sent to, and therefore will not garbage collected.
select as a kind of switch statement is a surprisingly clean syntax. It too uses randomness to insure that one channel doesn’t hog all the attention. I’m beginning to see a pattern of intentional randomness to help a program behave in a ''statistically consistent’ manor, and I approve. I haven’t seen this in a language before, or at least not to this degree. Sometimes bugs hide in the crevices of how a program folds together in its runtime behavior.  Randomness smooths and evens out this runtime behavior. This is a language feature that future languages should take note of.
time.Tick: Very useful function. Probably too useful. I can imagine this could be abused very easily.
labels / break to label: Dirty. Dirty. Dirty. Filthy.  
Concurrency: channels appear to have some strong consistency guarantees. However, anything outside of that is wild-west territory where the language user is given an arsenal of primitives and told not to shoot themselves in the foot. Disappointing. It probably would have been a better world if goroutines were segregated from each other except via channels (perhaps something like a copy on write fork, with channels being the sole ''shared resource’). Having access to unsynchronized shared memory and telling the language user to ''use responsibly’ means that go routines are much less powerful in practice than they could have been.
Example of the ugliness that arrises from weak concurrency design.
Lol. There is a -race flag to the compiler to instrument the runtime with checks for race conditions. I guess if the language makes it easy to have race conditions, then it is nice that it has a built in facility to try to detect them.
Use of blank imports for drivers: eh, feels kinda lame, but nicer than having an un ''unused’ import.
Wow. Go get actually speaks scm languages like git, and does things like clone when downloading. Way cool.
''Vendor’ directories: Hmmmmm…..My guess is that my opinion is going to change as I play more with the language. Initially, this seems like a very primitive way of handling dependency issues. Since there are no compiled artifacts (like jars) the source becomes how one integrates a 3rd party library. Nice in the sense that it demands one has access to the source code (which is a cannot be overstated wonderful feature), but bad in that it can get a bit unwieldy. Can’t imagine right now how multiple devs would coordinate, this might get ugly…
Built in testing framework: Cool that it has one, but it is a bit on the simple side. No doubt there are many frameworks that are better, but the built in one will most likely be a good enough place to start most of the time.
Example test functions: I like. I (and I’m sure most other devlopers) routinely create ''sandbox’ or ''playground’ code that is used to either explain or ''play with’ parts of a code base. I like that this has been formalized.
Reflection: Odd that they try to hide it like a dirty little secret. Obvious that the language designers feel this is dangerous territory.
Interesting that The Go Programming Language authors use converting Go data structures into Lisp S-Expressions as an example when discussing reflection, with no real description of what Lisp or S-Expressions are, just assuming that the reader is familiar. My suspicion is that this was at least semi-purposeful, to try to subtly make reflection seem a bit scarier than it is. A sort of gatekeeper. If you know Lisp we deem you worthy to use reflection. A bit elite-ish. It just so happens that I do know me some Lisp and am familiar with S-Expressions. So I guess I pass the test, but it is IMHO a childish game they are playing, and while I’m sure they felt they were either being clever or acting as responsible guardians, really they are just being dicks. What they should have done was use JSON since this is the modern equivalent of S-Expressions that many, many, many more people are familiar with.
Struct field tags: non-type-safe annotations. Looks like the only real way to use these is to parse them via convention. Too bad that they have to be read via reflection. Feels a bit tacked on at the last minute-ish. Useful but painful and error-prone.
Lots of ''we don’t have the space to show here’ in the book. A bit too much.
Unsafe: This is useful or not depending on the goal of the language. From an application development perspective: evil. From a systems programming language perspective: necessary. This is the dividing line. Since it can do unsafe stuff, Go is a systems programming language. But the goal seems to be to corral all the dangerous stuff into the unsafe package, to make it a useful application programming language as well. So how strong is that fence between the two?
Cgo: Whatever programming languages exist in a thousand years will have C bindings. Lots of details missing in the book, but the ''flavor’ of how it is done seems reasonable enough. I like accessing the c types via the ''C’ package, nicely done.
I find it telling that the final section of the book is a warning not to use reflection or unsafe. 
Summary of thoughts to this point:

Pragmatic. I don’t think anyone is going to call this language ''elegant’, but there is heavy emphasis on simplicity, combined with the clear intent to try to give the language user the tools needed to get the job done. It feels very much like a refined C for the modern era, with lots of extra safety and ease of use features, like garbage collection, and pointers sans pointer arithmetic.

Things I like:

General simplicity of the language combined with a slick tool chain make it very fast to get off the ground and running.
Null/nil as a valid ''zero value’ is a really nice idea that I hope more languages adopt in the future.
tuples for return values!
Finally, an example of a useable switch statement (other language designers THIS is how it should work).
Things I don’t like:

int/uint based on machine word size. This deserves a loud and forceful BOO! Might be bad enough to wreck the whole language for some.
Lack of error handling facilities.
Weak mechanisms for dealing with concurrency. Channels are an excellent start, but the road ends there, with too much work left to the language user.
Things that are AWESOME:

The built in opinionated source code formatting. 
Now armed with a sufficient amount of knowledge to be dangerous, I shall go forth and see what kind of Go-shaped nails need hammering. :)
