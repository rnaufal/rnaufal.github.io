---
author: admin
comments: true
date: 2010-09-07 19:31:08+00:00
layout: post
link: https://rafaelnaufal.com/blog/2010/09/07/singleton-in-java-with-enum-types/
slug: singleton-in-java-with-enum-types
title: Singleton in Java with Enum types
wordpress_id: 312
tags:
- effective java
- enum
- java
- joshua block
- serialization
- singleton
---

Java 1.5 introduced the concept of [Enum](http://download.oracle.com/javase/tutorial/java/javaOO/enum.html) types. They are type-safe constants, which implements `equals()`, `hashCode()` and cannot be extended.  Each constant can have attributes and override an abstract method created on each **Enum** class.

Although Singletons are not encouraged, the best way to create it is using **Enum** types. Here is an example:


    
    
    public enum Singleton {
        INSTANCE;
    
        public void sayHello() {
    	   System.out.println("Hello World!");
        }
    }
    



And then you call it this way:


    
    
    Singleton.INSTANCE.sayHello();
    



Using **Enums** to create Singletons brings the serialization mechanism already bundled in the **Enum** type. This technique is described on the [Effective Java Second Edition](http://java.sun.com/docs/books/effective/) book by Joshua Block.
