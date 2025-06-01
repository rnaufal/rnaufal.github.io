---
id: 76
title: 'Constructors in Scala'
guid: 'http://rnaufal.wordpress.com/?p=76'
dsq_thread_id:
    - '102750202'
categories:
    - Uncategorized
tags:
    - programming
    - scala
---

I just came across an interesting post by [Stephan Schmidt](http://codemonkeyism.com/) about [constructors in Scala](http://codemonkeyism.com/top-5-things-to-know-about-constructors-in-scala/).

It shows how to create constructors with immutable and mutable fields, how to have multiple constructors how to invoke super class constructors. I found it very handy and *concise* to create a constructor with a private immutable field:

`class Foo(private val bar: Bar)`