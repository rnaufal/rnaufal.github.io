---
id: 44
title: 'Do you need closures in Java?'
date: '2007-06-13T16:11:00-03:00'
guid: 'http://rnaufal.wordpress.com/2007/06/13/do-you-need-closures-in-java/'
lj_itemid:
    - '50'
lj_permalink:
    - 'http://rnaufal.livejournal.com/12803.html'
dsq_thread_id:
    - '104177147'
categories:
    - Uncategorized
tags:
    - java
    - oop
---

[TheServerSide](http://www.theserverside.com/news/thread.tss?thread_id=45189) has raised a question about whether [closures](http://en.wikipedia.org/wiki/Closure_(computer_science)) proposals to be implemented in the [Java](http://java.sun.com) language are really necessary. In my opinion, I think the Java language must be as it is, because:

- Generics syntax introduced in Java 1.5 are very difficult to understand and parse when code is read; mixing it with closures will keep the code a little messy;
- People would prefer to do things in the way they are used to, instead of learning a new construct in the language to implement their tasks (it’s better to focus on code maintenance and readability, after all, code is more read than written);
- Anonymous-inner classes are far less readable than inner classes, imagine when closures appear in such a code;

So, I think it’s better to maintain the language with the abstractions it already offers and focus on other improvements, like [reifiable](http://tech.puredanger.com/java7#reified) generics, that is, making generic type information available at runtime. And you? Will you think useful closures on the Java language?