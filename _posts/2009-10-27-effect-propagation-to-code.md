---
id: 126
title: 'Effect propagation to code'
guid: 'http://rafaelnaufal.com/blog/?p=126'
dsq_thread_id:
    - '104138827'
categories:
    - Uncategorized
tags:
    - code
    - java_programming
    - javase
    - legacy
    - testing
---

Reading Michael Feathers’ [‘Working Effectively With LegacyCode’](http://www.amazon.co.uk/Working-Effectively-Legacy-Robert-Martin/dp/0131177052/ref=sr_1_1?ie=UTF8&s=books&qid=1255440556&sr=8-1), I found quite interesting his heuristics to trace propagation of effects to code:

1. Identify a method that will change.
2. If the method has a return value, look at its callers.
3. See if the method modifies any values. If it does, look at the method that use those values, and the methods that use those methods.
4. Make sure you look for superclasses and subclasses that might be users of these instance variables and methods also.
5. Look at parameters to the methods. See if they or any objects that their methods return are used by the code that you want to change.
6. Look for global variables and static data that is modified in any of the methods you’ve identified.