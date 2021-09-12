---
author: admin
comments: true
date: 2009-08-27 01:15:40+00:00
layout: post
link: https://rafaelnaufal.com/blog/2009/08/26/constructors-in-scala/
slug: constructors-in-scala
title: Constructors in Scala
wordpress_id: 76
tags:
- programming
- scala
---

I just came across an interesting post by [Stephan Schmidt](http://codemonkeyism.com/) about [constructors in Scala](http://codemonkeyism.com/top-5-things-to-know-about-constructors-in-scala/).

It shows how to create constructors with immutable and mutable fields, how to have multiple constructors how to invoke super class constructors. I found it very handy and _concise_ to create a constructor with a private immutable field:

`class Foo(private val bar: Bar)`
