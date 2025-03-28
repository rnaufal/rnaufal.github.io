---
id: 33
title: 'Indicating the absence of an object'
date: '2006-11-15T23:41:00-02:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2006/11/15/indicating-the-absence-of-an-object/'
lj_itemid:
    - '39'
lj_permalink:
    - 'http://rnaufal.livejournal.com/10017.html'
dsq_thread_id:
    - '107669436'
categories:
    - Uncategorized
tags:
    - java
---

Sometimes I’ve seen some Java code intended to indicate the absence of parameters, that is, code validating **null** parameters (every public method must have a test to check against **null** parameter), verifying if a certain range is respected (like date, number ranges) and other kinds of [contextual](http://www.martinfowler.com/bliki/ContextualValidation.html) validation before calling the objects’ public methods. Some validation code (written in Java) is shown below:

At class Player:

> public void pickUp (Item item)  
> {  
>  assert(item != null): "item cannot be null";  
>  // some code here  
> }

The above code uses *Assertions*, introduced in JDK1.4, to validate the *item* parameter. If *item* is **null**, an *AssertionError* will be thrown with the message “item cannot be null”.

> public void drop (Item item)  
> {  
>  if(item == null) {  
>  throw new IllegalArgumentException(“item cannot be null”);  
>  }  
>  // some code here  
> }

This above one uses an *IllegalArgumentException*, which is a *RuntimeException*, to report a **null** *item*.

> public boolean addToInventory (Item item)  
> {  
>  if(item == null) {  
>  return false;  
>  }  
>  // some code here  
> }

And this above Java code snippet returns *false* if an *item* is **null**.

or, maybe, applying the [NullObject](http://www.mindspring.com/~mgrand/pattern_synopses.htm#Null%20Object) design pattern:

> class NullItem implements Item  
> {  
> }

and at Player it becomes:

> public void drop (Item item)  
> {  
>  // some code here  
> }

The last avoids a lot of tests to see if the parameter is **null**, replacing the tests with an object that provides the appropriate null behavior (*“do nothing”* behavior).  
The question is: which do you think is the best way to indicate the absence of such an object? Which do you use often? Tell me if you use another approach to report this.