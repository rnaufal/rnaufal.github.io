---
id: 34
title: 'Checked or Unchecked?'
date: '2006-12-10T21:42:00-02:00'
guid: 'http://rnaufal.wordpress.com/2006/12/10/checked-or-unchecked/'
lj_itemid:
    - '40'
lj_permalink:
    - 'http://rnaufal.livejournal.com/10413.html'
dsq_thread_id:
    - '108435245'
categories:
    - Uncategorized
tags:
    - java
---

Nice [post](http://www.mindview.net/Etc/Discussions/CheckedExceptions) from [Bruce Eckel](http://www.mindview.net/) about whether Java needs or not checked exceptions. I have to admit, I changed a lot my thougths about using checked exceptions in Java code with this post. He explains why it’s better to use unchecked exceptions instead of checked ones with some good arguments, like the possibility to swallow the exception inside an empty *catch* block and loose the stack trace information. The programmer is tempted to swallow the exception because he’s forced to catch it and write reams of code around the exception. Bruce also states, emphasizing the use of unchecked exceptions:

> “If I want to catch the exception, I can, but I’m not tempted to swallow it just to avoid writing reams of code. If I don’t’ want to write around the exceptions, I ignore them, and if one comes up it gets reported to me during debugging, and I can decide how to handle it then. I still deal with the exception, but I’m not forced to write a bunch of code about exceptions all the time.”

I think there’s a tendency to apply checked exceptions because people are used to static type checking, people are afraid to catch errors at runtime, static type programming languages forces this. People from [Python](http://www.python.org/), [Ruby](http://www.ruby-lang.org/en/) are used to the unchecked approach, because those languages are dynamically typed, so, there’s no pain :-). Now I prefer to use unchecked exceptions rather than checked ones because I agree with Bruce’s arguments and I’m moving my thoughts forward to dynamically typed languages. And you, what do you think about using checked / unchecked exceptions? Do you have a different opinion?