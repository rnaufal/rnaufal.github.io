---
id: 58
title: 'Is Java on a evolutionary dead end way?'
guid: 'http://rnaufal.wordpress.com/2008/01/11/is-java-on-a-evolutionary-dead-end-way/'
lj_itemid:
    - '66'
lj_permalink:
    - 'http://rnaufal.livejournal.com/17078.html'
dsq_thread_id:
    - '103528902'
categories:
    - Uncategorized
tags:
    - closures
    - eckel
    - java
    - programming
    - scala
---

[Artima](http://www.artima.com) is running an [article](http://www.artima.com/weblogs/viewpost.jsp?thread=221903) where [Bruce Eckel](http://www.mindview.net) talks about about [Java’s](http://www.java.sun.com) objective on *backwards compatibilities* and the problem of *combinatorial complexity* when you combine a new feature in every possible way with the other language features already present.

> It’s the *combinatorial complexity* that you get when you combine a new feature in every possible way with the other language features. The combinatorial complexity can produce horrifying surprises, typically after the feature is added when it’s too late to do anything about it.

It’s clear Eckel is mentioning the Java [closures’](http://en.wikipedia.org/wiki/Closure_(computer_science)) proposals to become part of the language on the Java 7 and the major improvements occured when Java 5 appeared.

> If Java is unwilling to break backwards compatibility, then it is inevitable that it will acquire both unproductive complexity and incomplete implementation of new features. I’ve made the case in *Thinking in Java 4e* that Java Generics are only a pale imitation of real generics, and one of the more appealing suggestions for closures is an incomplete implementation of true closures, but it would actually be preferable to a complete implementation because it produces clearer, more straightforward code.

 I particularly agree with him, when he also says

> Fundamental new features should be expressed in new languages, carefully designed as part of the ecosystem of a language, rather thanbeing inserted as an afterthought.

 He also considers [Scala](http://www.scala-lang.org/index.html) as an alternative for the Java language. Eckel also declares

> Java values backward compatibility over the clarity of its abstractions.

 I don’t agree with him at this later point, the [Collections’](http://java.sun.com/docs/books/tutorial/collections/index.html) framework is an example of good API design rules with a lot of well designed abstractions by [Joshua Block](http://en.wikipedia.org/wiki/Joshua_Bloch), *separating things that change from things that stay the same*.

And you? What do u think about it? Should Scala be considered as an exit for Java?