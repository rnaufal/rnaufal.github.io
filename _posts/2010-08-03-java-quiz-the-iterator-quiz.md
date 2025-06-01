---
id: 267
title: 'Java-Quiz: The Iterator Quiz'
guid: 'http://rafaelnaufal.com/blog/?p=267'
dsq_thread_id:
    - '125658658'
categories:
    - Uncategorized
tags:
    - iterator
    - java
    - java_programming
    - quiz
---

Danilo sent us an interesting Java-Quiz from the [Java Specialists’ Newsletter](http://www.javaspecialists.eu/archive/Issue186.html) created by Olivier Croisier. You have to insert your corrective code in place of the `//FIXME` comment, following these instructions:

1. Do not modify his existing code, it’s Perfect (of course).
2. The FIXME tag shows where you’re allowed to insert your corrective code
3. He must be able to understand your solution when he comes back (so using Reflection is not an option).

Can you find a solution for it?

{% raw %}
```java
final List<String> list = new ArrayList() {{ 
      add("Hello");
}};
final Iterator<String> iterator = list.iterator();
System.out.println(iterator.next());
list.add("World");
// FIXME : work here while I'm sunbathing
System.out.println(iterator.next());
```
{% endraw %}

Later I’ll post my attempt to solve it.