---
author: admin
comments: true
date: 2009-09-23 02:45:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2009/09/22/jdk7-tackles-java-verbosity/
slug: jdk7-tackles-java-verbosity
title: JDK7 Tackles Java Verbosity
wordpress_id: 86
tags:
- collections
- java
- lists
- literals
- maps
- programming
- scala
- sets
---

Interesting [article](http://java.dzone.com/articles/jdk7-tackles-java-verbosity) showing some changes on the Java platform to address its verbosity, but keeping code readability safe. 
I liked the new Collection's literals syntax to create lists, sets and maps:



<blockquote>`List powersOf2 = {1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024};`
`Map ages = {"John" : 35, "Mary" : 28, "Steve" : 42};`</blockquote>



Although it can be possible to use the [DoubleBraceInitialization](http://c2.com/cgi/wiki?DoubleBraceInitialization) idiom to initialize collections in a more elegant way, this syntax is very terse and concise.

BTW, as I [said](http://rafaelnaufal.com/blog/?p=73#comments) before, [Scala](http://www.scala-lang.org) already has a syntactic sugar to create a literal Map:



<blockquote>`val ages = Map("John" -> 35, "Mary" -> 28,  "Steve" -> 42)`</blockquote>



Maybe this change was taken into account considering the Scala collection literals implementation?
