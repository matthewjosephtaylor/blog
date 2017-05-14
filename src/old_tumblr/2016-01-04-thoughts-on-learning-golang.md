---
layout: post
title: Thoughts on learning Golang
date: '2016-01-04T09:35:35+00:00'
tags: []
tumblr_url: http://www.matthewjosephtaylor.com/post/136610735879/thoughts-on-learning-golang
---
My initial impetus for learning go is to get more familiar with the internals of docker, because it seems that I’m going to have to rewrite their registry service to suit my desires. Also, because learning new languages is just kind of a fun thing to do, and Go appears to have enough traction now to make it worth the effort.

Youtube video I recommend: Go Programming in One Hour

Book I’m currently reading: The Go Programming Language by Donovan & Kernighan

Here is an unordered list random thoughts as I go about the learning process:

Why does the type come after the variable name? I get the feeling this was done for no real reason other than to make it look different.
gofmt is actually pretty darn cool. I like the tabs, would have preferred the semicolons.
Pointers without pointer arithmetic. I think this is a good balance.
My first impression is that it feels a lot like C but without a lot of the accounting (memory management).
Having things like ‘new’ not be a keyword, and thus giving the language user the ability to shadow them seems dangerous, and I’m not sure why this was done. (At first glance I would call it a horrible design, but maybe it makes sense later on).
There doesn’t seem to be a way to specify a method while defining a struct (but you can attach a method to a struct later). Perhaps there is a way of doing this but just haven’t discovered yet. 
I like the approach of creating small command line tools for refactoring and static analysis. Will give more lightweight editors the power one expects from a more full fledged IDE without the overhead. Very nice.
atom with the go-plus plugin works well, at least for playing around.
Channels are very unixy and I like.
Mutexes for synchronization, not so sexy. 
int and uint are different depending on machine architecture == EVIL. This is a major flaw in C and I’m shocked to see the mistake repeated. This just causes lots of porting headaches for no real benefit to anyone, for relatively minor performance gain. Worse because people are going to naturally migrate to using these (because the name is short/easy/intuitive) they are going to use it by default, and be bitten. I’m just going to state that use of int/uint in golang broken by design and should never be used which is a shame. The MEANING of a type should not change based on where it is run. Utterly stupid design decision. They should have just used a name like ''word’ / ''uword’ for the 100 people on the planet who will actually know how to, and need to, use this type. Instead 100,000 developers are now doomed to writing ''int64’ where they should have had the freedom of writing ''int’ (who am I kidding?  10,000 devs will write ''int64’, and 90,000 devs will use ''int’ without a care or clue, until their code mysteriously breaks in weird ways depending on where it is run).
I like the name of ''rune’ for a unicode code point. (does not make up for int/uint)
There is a specific ''complex32/64’ type.  Neat.
Immutable Strings. This seems familiar. Wonder if this was designed this way to help memory/garbage collection or for program correctness.
untyped constants: weird. Don’t see the need for this. The weirdness boils down to var x = 0 being an ''int’ type, and var x = 0.0 being a float64 type because the zeros are untyped constants whose values are determined as needed.  So the gotcha is that var x = 0 shouldn’t be used as it will default to the badly designed ''int’ type.
Not sure how I feel about float64(x) as a conversion syntax.  On the one hand it seems nice because it looks like a function, on the other hand it seems confusing…because it isn’t really a function.
Tuples are awesome!
Using tuples for error handling is ugly! WTF? This feels like a very C-like way of error handling, and really should have been rethought. Feels like there was a disagreement on how to do error handling, and so the committee decision was to not deal with it and make it ugly for everyone. Not cool.
Enums (lack of): Should have just done it right with the type of an enum being a string value. The way they are ''suggested’ to be done via struct/iota feels like a performance hack, that will serve almost no-one well over the long term.
Arrays are passed via copy rather than reference. Can pass reference via pointers. Not good or bad, just something to consider.
Slices are nice, but not being able to determine implementation of backing array could lead to not being able to use them when performance becomes critical. Definitely a case where one size isn’t likely to fit all…but might fit most?
Ugly design that range’s output is index, value.  Should have been value, index.  value is 100x more useful than index when looping, so most code is going to have _, val = range x.
No slice equality comparison via ’==’ like there is with array: This should be a thing. No reason not to implement it at least as a reference check, if one is going to have == mean that individual values are checked in arrays. Perhaps a good case for why ’===’ should be a thing, or a case why == for array shouldn’t be a thing.
No set type. Disappointing.
Overall the collection types seem a bit weak. Probably libraries are expected to fill this role.
Interesting use of tuples to get around the ''null value’ problem for maps. Not sure I like it, but it’s interesting.
Zero values instead of nil/null : Sensible. I think I like, almost certainly I should like. But have I been drinking the poison of null values for so long that I’ve actually acquired a taste for them? Feels a bit limiting somehow. Like a dimension is missing. Definitely one of the better design decisions of the language (Not that the outcome is guaranteed be good, just that it is indeed different than other similar languages, and has a solid grounding on why it could be a good decision, unlike silly things like changing the order of variable name/type name), will be interesting to see how it works in practice.
Struct equality: Simplistic. I really wish there was an Equals() interface method that the equality operator would use if it found one.  I’m starting to think that the comparison operators are a bit weak in general (can they be fixed via 3rd party libraries?)
Did some code experiments: Slices and Maps pass via reference, arrays pass via copy, an odd inconsistency.
Built in templating is kinda neat. Arguably not the sort of thing that should be in the core library, but perhaps useful enough to justify.
Wow, stack size grows dynamically up to 1GB. Wonder if that causes issues with recursion gone wild? Sometimes a smaller stack size can be nice, because a 1GB stack is almost certainly not going to be intended.
Named return values in the method signature are kinda neat. Especially in cases of returning a tuple I can see that as a really nice thing to have, at least as far as documentation.
Yeah, really not buying the philosophy behind error handling.  Perhaps I’ll be brought onboard, but for now it looks like there is some sort of irrational fear of exceptions. If they came up with something different maybe I could swallow it better, but just returning the error as another kind of data and forcing the language user into writing millions if err!=nil statements just feels draining and stupid. Like democracy, exceptions might be the worst option, except all the others, and if they couldn’t think of a better idea they probably should just have swallowed their pride and used them anyway, instead of voting for no built-in error handling mechanism.
Closures. Yummy.
There seems to be several gotchas with scoping and defining variables that accidently shadow a variable in a higher scope. This could have been solved by simply making it illegal to shadow these variables by defining that only one variable of a name per scope. Why wasn’t this done?
defer is a novel and interesting idea, but it feels like the real answer should be that resources should be garbage collected (closed) as soon as their ''interface object’ goes out of scope. Like memory management, resource management is mostly just accounting and should be handed off to the compiler/runtime to take care of. Destructors or an optional ''Close’ method interface would be a better fit.
Using defer for execution tracing is pretty nifty.
Disappointing that stack traces only have line numbers (line position is sometimes just as important), but glad that they exist. 
Named receivers (naming ''this’ object) : Not an immediate fan. Why was this thought to be a good idea? Seems more like a hold-over from a time when Go was being developed and they were having a fight about if the language should have objects. I’ve never wanted to rename ''this’, seems like it would just cause confusion, and extra brain power required remembering what the ''this’ object is named complexity. Yeah, just a bad idea. Going to declare that the receiver object should always be called a consistent predetermined name (I vote ''this’) and that any convention that suggests otherwise is just being different for the sake of being stupid (unlike reversing the type/variable name convention which is just different purely for the sake of being different but isn’t likely to cause nearly as many programming mistakes).
Seems that the style guide doesn’t like you to name the receiver certain things: ’“receiver name should be a reflection of its identity; don’t use generic names such as "me”, “this”, or “self”’ What a bunch of BS. Whatever you do make sure you don’t call it what 99% of the OO world calls this thing.  I think this fight just went from stupid to idiotic. It’s one thing to allow you to call it something ugly and confusing, it is another thing entirely to officially call it ''bad style’ to call it anything but what it everyone else on the planet calls it. This is going to be my goto example of where a relatively small, but bad, language design decision can get ballooned into a cult of bad practice. The idea of being different to be purposefully worse is kind of mind blowing. 
Why would anyone want a non-pointer receiver? I guess it is effectively sort of like a static method, only the ''static method’ has access to a copy of the receiver. I guess I can see cases where that could be useful to guarantee read-only access to the receiver object. 
Implicit dereferencing feels a bit hokey and I can imagine there are cases where one is fighting the compiler, but maybe not.
Nil/Null receivers as valid objects: I think this might be genius. Allows for ''null’ objects to have a well defined/meaningful state. The implementation seems more pragmatic than elegant (methods have to explicitly check for nil of the receiver object) but the idea itself is a definite ''aha’ moment. This is definitely one of the golden treasures of this language to be noted and praised.
Embedding of types (especially unamed structs): An interesting way to do composition. Reminds me a bit of Ruby’s mixins. Solves the multiple name collision problem by having a unique path for ambiguous names, but allows you to use the ''shortcut’ short names where they are unique.   Will reserve judgement. Need to see in real world practice how this gets used/abused. Definite points for creativity, and possibly a good solution to the problem.
I’m about ½ way through the book, haven’t got to the juicy stuff like refleciton yet.  So far my overall impression is that this is going to be a good language for writing small portable command line programs, and maybe other things as well, but maybe not more complex programs where the language’s lack of features might start to hurt more than help.  Definitely more impressed after leaning about the language, than before I started the journey.
