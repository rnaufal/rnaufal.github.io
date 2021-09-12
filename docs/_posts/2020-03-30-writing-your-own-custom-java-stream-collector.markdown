---
author: rnaufal
comments: true
date: 2020-03-30 00:37:17+00:00
layout: post
link: https://rafaelnaufal.com/blog/2020/03/29/writing-your-own-custom-java-stream-collector/
slug: writing-your-own-custom-java-stream-collector
title: Writing your own custom Java stream collector
wordpress_id: 723
categories:
- collections
- collectors
- development
- functional
- java
- jdk14
- lambdas
- programming
- streams
tags:
- collections
- collectors
- development
- functional
- java
- jdk14
- lambdas
- programming
- streams
---




One of the common operations of the [Collectors](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/Collectors.html) API introduced in [Java 8](http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk8-downloads-2133151.html) is the possibility to collect results into a result container like [List](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/List.html), [Set](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/Set.html) or [Map](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/Map.html). The following example uses the <code>[collect()](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/IntStream.html#collect(java.util.function.Supplier,java.util.function.ObjIntConsumer,java.util.function.BiConsumer))</code> method to generate a <code>[HashSet](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/HashSet.html)</code> containing unique numbers:











Now suppose a given string and the need to compute some summaries on it, like the number of uppercase, lowercase, invalid chars and how many digits are present on that string.







Applying a reduce operation on each needed summary operation would result in more than one pass through the data, like this (here I am using the [var](https://developer.oracle.com/java/jdk-10-local-variable-type-inference.html) keyword introduced in [Java 10](https://www.oracle.com/java/technologies/java-archive-javase10-downloads.html)):











In the above code excerpt we are iterating three times through the string to compute the summaries. If we want to iterate just one time on the give string and get the desired results, we could fallback to the traditional imperative approach:











Despite the solution above, there is another one: writing your own custom stream collector.  This custom collector can compute the number of uppercase, lowercase, invalid chars and how many digits are present on the given string, in a single pass through the data. It is possible to make it run in <code>parallel</code> with the [Streams](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/Stream.html) API as well.







The custom stream collector shown here uses the <code>[chars()](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#chars())</code> method of the [String](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html) class which returns an [IntStream](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/IntStream.html). The <code>IntStream</code> class contains a <code>collect()</code> method that computes a mutable reduction on the elements and returns its result in a container class.







The next example shows the container class code. It receives and accumulates each <code>char</code> of the String in the <code>accept()</code> method,  thus categorizing it as a digit, uppercase char, lowercase char or as an invalid char. 











The complete implementation of the [collect()](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/IntStream.html#collect(java.util.function.Supplier,java.util.function.ObjIntConsumer,java.util.function.BiConsumer)) method which produces the  result of the reduction in the [CharSummaryStatistics](https://github.com/rnaufal/blog/blob/master/summaries/src/main/java/br/com/rnaufal/summaries/CharSummaryStatistics.java) class is shown below. As a new char arrives, it is categorized in the <code>CharSummaryStatistics.accept()</code> method. The <code>CharSummaryStatistics.combine()</code> method is used to merge partial results.











Have you ever written a custom Java stream collector? Please drop your comments here.







The complete source code can be found on [GitHub](https://github.com/rnaufal/blog/tree/master/summaries).







As a reference for writing this post,  this [article](https://developer.ibm.com/articles/j-java-streams-2-brian-goetz/) is part of a series about [Streams](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/Stream.html) and it is a good reference for learning how to aggregate and collect with Streams. All the articles from this series about Streams can be found [here](https://developer.ibm.com/series/java-streams/).



