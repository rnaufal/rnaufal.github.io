---
author: admin
comments: true
date: 2006-11-16 02:41:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/11/15/indicating-the-absence-of-an-object/
slug: indicating-the-absence-of-an-object
title: Indicating the absence of an object
wordpress_id: 33
tags:
- java
---

Sometimes I've seen some Java code intended to indicate the absence of parameters, that is, code validating **null** parameters (every public method must have a test to check against **null** parameter), verifying if a certain range is respected (like  date, number ranges) and other kinds of [contextual](http://www.martinfowler.com/bliki/ContextualValidation.html) validation before calling the objects' public methods.  Some validation code (written in Java) is shown below:

At class Player:



<blockquote>
public void pickUp (Item item) 
{
assert(item != null): "item cannot be null";
// some code here
}
</blockquote>



The above code uses _Assertions_, introduced in JDK1.4, to validate the _item_ parameter. If _item_ is **null**, an _AssertionError_ will be thrown with the message "item cannot be null".



<blockquote>
public void drop (Item item) 
{
if(item == null) {
throw new IllegalArgumentException("item cannot be null"); 
}
// some code here
}
</blockquote>



This above one uses an _IllegalArgumentException_, which is a _RuntimeException_, to report a **null** _item_.



<blockquote>
public boolean addToInventory (Item item) 
{
if(item == null) {
return false;
}
// some code here
}
</blockquote>



And this above Java code snippet returns _false_ if an _item_ is **null**. 

or, maybe, applying the [NullObject](http://www.mindspring.com/~mgrand/pattern_synopses.htm#Null%20Object) design pattern:



<blockquote>
class NullItem implements Item 
{
}
</blockquote>



and at Player it becomes:



<blockquote>
public void drop (Item item) 
{
// some code here
}
</blockquote>



The last avoids a lot of tests to see if the parameter is **null**, replacing the tests with an object that provides the appropriate null behavior (_"do nothing"_ behavior).
The question is: which do you think is the best way to indicate the absence of such an object? Which do you use often? Tell me if you use another approach to report this.
