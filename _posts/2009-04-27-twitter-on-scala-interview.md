---
id: 71
title: 'Twitter on Scala Interview'
guid: 'http://rnaufal.wordpress.com/2009/04/27/twitter-on-scala-interview/'
lj_itemid:
    - '80'
lj_permalink:
    - 'http://rnaufal.livejournal.com/20482.html'
dsq_thread_id:
    - '102752182'
categories:
    - Uncategorized
tags:
    - java
    - ruby
    - scala
    - threads
    - twitter
---

There is a nice [interview](http://www.artima.com/scalazine/articles/twitter_on_scala.html) with the [Twitter](http://www.twitter.com) development team on Artima about using Scala in production on Twitter code. The team talks about some issues and facilities regarding the chose of Scala to develop Twitter’s queueing system and how Scala affected the team’s programming style.

My personal highlights:

> And Ruby, like many scripting languages, has trouble being an environment for long lived processes. **But the JVM is very good at that, because it’s been optimized for that over the last ten years**..

> So Scala provides a basis for writing long-lived servers…Another thing we really like about Scala is static typing that’s not painful. Sometimes it would be really nice in Ruby to say things like, here’s an optional type annotation

> And because **Ruby’s garbage collector is not quite as good as Java’s**, each process uses up a lot of memory. We can’t really run very many Ruby daemon processes on a single machine without consuming large amounts of memory

> In some cases we just decided to burrow down and use the **Java collections from Scala, which is a nice advantage of Scala**, that we have that option..

> As I’ve learned more Scala I’ve started thinking more functionally than I did before. When I first started I would use the for expression, which is very much like Python’s. Now more often I find myself invoking `map` or `foreach` directly on iterators..

> The reason you should care about immutability is that **if you’re using threads and your objects are immutable, you don’t have to worry about things changing underneath you**..

It’s very worth read. Post your comments here when you read it.