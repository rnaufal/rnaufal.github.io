---
id: 64
title: 'The Fan programming language'
guid: 'http://rnaufal.wordpress.com/2008/06/12/the-fan-programming-language/'
lj_itemid:
    - '72'
lj_permalink:
    - 'http://rnaufal.livejournal.com/18513.html'
lj_current_mood:
    - sleepy
categories:
    - Uncategorized
tags:
    - fan
    - functional
    - oop
    - programming_languages
---

[Cedric](http://beust.com/weblog/archives/000488.html) has showed us an interesting programming language called [Fan](http://www.fandev.org/), which has a lot of useful features. The ones I liked most are:

- **Familiar Syntax:** Java and C# programmers will feel at home with Fan’s curly brace syntax.
- **Concurrency:** Tackle concurrency with built-in immutability, message passing, and REST oriented transactional memory.
- **Static and Dynamic Typing:** Don’t like the extremes – take the middle of the road.
- **Object Oriented:** Everything is an object.
- **Functional:** Functions and closures are baked in.

Here are some code chunks, showing its closures syntax:

> // find files less than one day old  
> files := dir.list.findAll |File f-&gt;Bool|  
> {  
>  return DateTime.now – f.modified &lt; 1day  
> }
> 
> // print the filenames to stdout  
> files.each |File f|  
> {  
>  echo("$f.modified.toLocale: $f.name")  
> }

I haven’t tried the Fan language a lot yet (I’ll post my comments here when I do it), but I congratulate the Fan authors for being possible to run it on both the JVM and .Net. I agree with Cedric when he said about the possibility to declare constructors with arbitrary names (although they must be prefixed with the **new** keyword) and invoke it as static methods of the class. From designer of the class point of view, it’s easy to identify the constructor (it’s highlighted by the **new** keyword), but from the client it’s difficult because there’s no way to differentiate a constructor from a static method call. It’s a bit odd to be able to do that. Just take a look at the code:

> // Using an arbitrary name as a constructor  
> class Person  
> {  
>  new create(Int age) { this.age = age; }  
>  Int age  
> }  
> p = Person.create(20)

Anyway, I think it’s a good work to make the language have both object-oriented and functional constructs and be portable to both the Java VM and the .NET CLR. Good work guys!