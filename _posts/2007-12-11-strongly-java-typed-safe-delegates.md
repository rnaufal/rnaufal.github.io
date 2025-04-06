---
id: 56
title: 'Strongly Java typed safe delegates'
date: '2007-12-11T22:57:00-02:00'
guid: 'http://rnaufal.wordpress.com/2007/12/11/strongly-java-typed-safe-delegates/'
lj_itemid:
    - '64'
lj_permalink:
    - 'http://rnaufal.livejournal.com/16456.html'
dsq_thread_id:
    - '103767249'
categories:
    - Uncategorized
tags:
    - delegate
    - java
    - programming
    - type_safe
---

This great post explores an interesting Java implementation about using the delegate programming feature, in a type safe way. Delegate is a form of function pointer, commonly used to implement callbacks. It specifies a method to call, which is dispatched in runtime. From [Wikipedia](http://en.wikipedia.org/wiki/Delegation_(programming)), we have:

> The short definition is that delegation defines method dispatching the way it is defined for virtual methods in inheritance: It is always the most specific method which is chosen during method-lookup – Hence it is the **original** receiver entity which is the start of method lookup even though it has passed on control to some other object(through a delegation link, not an object reference). Delegation has the advantage that it can take place at run-time and affect only a subset of entities of some type and can even be removed at run-time. Inheritance on the other hand typically targets the type rather than the instances and is restricted to compile time.

We almost know weakly typed Java delegate implementations, relying upon Strings to delegate to named methods. This way, it lets you mistype the method name easily and it also does not not allow method completion in the IDE. [Alex](http://weblogs.java.net/blog/alexwinston/archive/2005/04/strongly_types_1.html) shows us a type-safe Java delegate implementation, which enhances readibility and supports code completion on the IDE, using the [cglib](http://cglib.sourceforge.net/) dynamic proxy facility. The article is very worth reading. As a developer on a daily basis I’ve never seen a concrete use of this programming feature, despite being very interesting. Have you ever used the delegate feature?