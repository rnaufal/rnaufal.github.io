---
id: 86
title: 'JDK7 Tackles Java Verbosity'
date: '2009-09-22T23:45:00-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=86'
dsq_thread_id:
    - '102911457'
categories:
    - Uncategorized
tags:
    - collections
    - java
    - lists
    - literals
    - maps
    - programming
    - scala
    - sets
---

Interesting [article](http://java.dzone.com/articles/jdk7-tackles-java-verbosity) showing some changes on the Java platform to address its verbosity, but keeping code readability safe.  
I liked the new Collection’s literals syntax to create lists, sets and maps:

```java
List powersOf2 = {1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024};  
Map ages = {"John" : 35, "Mary" : 28, "Steve" : 42};
```

Although it can be possible to use the [DoubleBraceInitialization](http://c2.com/cgi/wiki?DoubleBraceInitialization) idiom to initialize collections in a more elegant way, this syntax is very terse and concise.

BTW, as I [said](http://rafaelnaufal.com/blog/?p=73#comments) before, [Scala](http://www.scala-lang.org) already has a syntactic sugar to create a literal Map:

```scala
val ages = Map("John" -> 35, "Mary" -> 28,  "Steve" -> 42)
```

Maybe this change was taken into account considering the Scala collection literals implementation?