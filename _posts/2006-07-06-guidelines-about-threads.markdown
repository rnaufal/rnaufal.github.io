---
author: admin
comments: true
date: 2006-07-06 17:29:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/07/06/guidelines-about-threads/
slug: guidelines-about-threads
title: Guidelines about threads
wordpress_id: 17
tags:
- java
---

From _[Bruce Eckel's Thinking in Java](http://mindview.net/Books/TIJ4)_ book, about [threads](http://en.wikipedia.org/wiki/Thread_%28computer_science%29):





  1. If you need to synchronize one method in a class, synchronize all of them. It’s often difficult to tell for sure if a method will be negativelyaffected if you leave synchronization out. 



  2. Be extremely careful when removing synchronization from methods. The typical reason to do this is for performance, but in JDK 1.3 and 1.4 the overhead of **synchronized** has been greatly reduced. In addition, you should only do this after using a profiler to determine that **synchronized** is indeed the bottleneck. 


