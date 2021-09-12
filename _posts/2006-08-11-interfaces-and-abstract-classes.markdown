---
author: admin
comments: true
date: 2006-08-11 02:47:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/08/10/interfaces-and-abstract-classes/
slug: interfaces-and-abstract-classes
title: Interfaces and Abstract classes
wordpress_id: 23
tags:
- java
---

My friend [bruno](http://bpfurtado.livejournal.com/23707.html) started a thread about interfaces and abstract classes and I wanna continue here. I totally agree with his points and I'm adding other ones here. About interfaces:  



  1. define a communication "protocol"  between classes.
It is, a class which has an interface as a colaborator knows which operations it can send messages for this interface;

  2. isolate the clients from the implementation.
So, you are free to change the internal structure of your implementation and the clients don't have to concern with this. So, we are applying the hiding mechanism here, known as [encapsulation](http://en.wikipedia.org/wiki/Implementation_Hiding);

  3. clients don't have to concern with implementation details, because they only work with the interface. The real type doesn't care for the client;


  4. define the form for a class. More precisely, is what the classes look like while the implementation says how the classes work.

About abstract classes:  



  1. describe an incomplete abstraction definition, as interfaces do;


  2. define a common _interface_ for all the subtypes;


  3. establish a basic form, so it's easy to say what's in common between the subtypes;


  4. express only a interface, not a particular implementation

Interfaces and abstract classes are ways of managing the internal coupling of your code. You create them when you want to manipulate classes through this common interface. If you only want to factor behavior, interfaces are a good choice, but if you want to factor structure too, choose abstract classes.
