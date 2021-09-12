---
author: admin
comments: true
date: 2006-07-18 23:15:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/07/18/thread-groups/
slug: thread-groups
title: Thread Groups
wordpress_id: 20
tags:
- java
---

Some months ago I was wondering what was the benefit of using _thread groups_, which is a container of threads in Java.  Reading [Bruce Eckel's Thinking in Java](http://mindview.net/Books/TIJ4), I discovered this quote from [Joshua Block](http://java.sun.com/docs/books/effective/), the one who improved the [Collections framework](http://java.sun.com/docs/books/tutorial/collections/index.html) in JDK 1.2:

_"Thread groups are best viewed as an unsuccessful experiment, and you may simply ignore their existence.”_

I haven't been told about any Sun's official statement about this topic before reading the book. So, why do they let us spend our effort trying to figure out the value of thread groups? :-)
