---
author: admin
comments: true
date: 2008-01-11 03:31:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2008/01/11/is-java-on-a-evolutionary-dead-end-way/
slug: is-java-on-a-evolutionary-dead-end-way
title: Is Java on a evolutionary dead end way?
wordpress_id: 58
tags:
- closures
- eckel
- java
- programming
- scala
---

[Artima](http://www.artima.com) is running an [article](http://www.artima.com/weblogs/viewpost.jsp?thread=221903) where [Bruce Eckel](http://www.mindview.net) talks about about [Java's](http://www.java.sun.com) objective on _backwards compatibilities_ and the problem of _combinatorial complexity_ when you combine a new feature in every possible way with the other language features already present.



<blockquote>It's the _combinatorial complexity_ that you get when you combine a new feature in every possible way with the other language features. The combinatorial complexity can produce horrifying surprises, typically after the feature is added when it's too late to do anything about it.</blockquote>


It's clear Eckel is mentioning the Java [closures'](http://en.wikipedia.org/wiki/Closure_(computer_science)) proposals to become part of the language on the Java 7 and the major improvements occured when Java 5 appeared.



<blockquote>If Java is unwilling to break backwards compatibility, then it is inevitable that it will acquire both unproductive complexity and incomplete implementation of new features. I've made the case in _Thinking in Java 4e_ that Java Generics are only a pale imitation of real generics, and one of the more appealing suggestions for closures is an incomplete implementation of true closures, but it would actually be preferable to a complete implementation because it produces clearer, more straightforward code.</blockquote>

I particularly agree with him, when he also says 

<blockquote>Fundamental new features should be expressed in new languages, carefully designed as part of the ecosystem of a language, rather thanbeing inserted as an afterthought.</blockquote>

He also considers [Scala](http://www.scala-lang.org/index.html) as an alternative for the Java language. Eckel also declares 

<blockquote>Java values backward compatibility over the clarity of its abstractions.</blockquote>

I don't agree with him at this later point, the [Collections'](http://java.sun.com/docs/books/tutorial/collections/index.html) framework is an example of good API design rules with a lot of well designed abstractions by [Joshua Block](http://en.wikipedia.org/wiki/Joshua_Bloch), _separating things that change from things that stay the same_.

And you? What do u think about it? Should Scala be considered as an exit for Java?
