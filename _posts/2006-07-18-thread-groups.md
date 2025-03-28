---
id: 22
title: 'Thread Groups'
date: '2006-07-18T20:15:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2006/07/18/thread-groups/'
lj_itemid:
    - '17'
lj_permalink:
    - 'http://rnaufal.livejournal.com/4499.html'
dsq_thread_id:
    - '102751753'
categories:
    - Uncategorized
tags:
    - java
---

Some months ago I was wondering what was the benefit of using *thread groups*, which is a container of threads in Java. Reading [Bruce Eckel’s Thinking in Java](http://mindview.net/Books/TIJ4), I discovered this quote from [Joshua Block](http://java.sun.com/docs/books/effective/), the one who improved the [Collections framework](http://java.sun.com/docs/books/tutorial/collections/index.html) in JDK 1.2:

<font face="Georgia">*“Thread groups are best viewed as an unsuccessful experiment, and you may simply ignore their existence.”*</font>

I haven’t been told about any Sun’s official statement about this topic before reading the book. So, why do they let us spend our effort trying to figure out the value of thread groups? 🙂