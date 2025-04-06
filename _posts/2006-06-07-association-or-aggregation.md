---
id: 10
title: 'Association or Aggregation?'
date: '2006-06-07T10:27:00-03:00'
guid: 'http://rnaufal.wordpress.com/2006/06/07/association-or-aggregation/'
lj_itemid:
    - '5'
lj_permalink:
    - 'http://rnaufal.livejournal.com/1476.html'
dsq_thread_id:
    - '102825398'
categories:
    - Uncategorized
tags:
    - software
---

I’ve been discussing with my co-workers when we have to use Aggregation or Association in UML models. [Martin Fowler](http://www.martinfowler.com/) in [UML Distilled, 3rd Edition](http://www.bookpool.com/sm/0321193687) says aggregation is the *part-of* relationship. It’s like saying that a car has an engine and 4 wheels as its parts. But aggregation was included in UML to differentiate from association, because in pre-UML days people didn’t knowhow to differentiate them. But aggregation, as Fowler says, is meaningless. [Jim Rumbaugh](http://en.wikipedia.org/wiki/James_Rumbaugh) says “Think of aggregation as a modeling placebo”. Association is a way to notate a property in our classes, but you don’t manage the life cycle of the associated property, as the aggregation relationship do. The solid line between the classes define the way one instance of the associating class can execute methods (operations realizations) of the associated object. So, why to use aggregation?