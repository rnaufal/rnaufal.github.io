---
id: 732
title: 'Writing your own custom Java stream collector'
date: '2022-12-17T12:29:02-03:00'
author: rnaufal
layout: revision
guid: 'https://rafaelnaufal.com/?p=732'
---

One of the common operations of the [Collectors](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/Collectors.html) API introduced in [Java 8](http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk8-downloads-2133151.html) is the possibility to collect results into a result container like [List](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/List.html), [Set](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/Set.html) or [Map](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/Map.html). The following example uses the `<a href="https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/IntStream.html#collect(java.util.function.Supplier,java.util.function.ObjIntConsumer,java.util.function.BiConsumer)">collect()</a>` method to generate a `<a href="https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/HashSet.html">HashSet</a>` containing unique numbers:

<script src="https://gist.github.com/rnaufal/98eb7b5c29f7bae46612158ea3b1c934.js"></script>Now suppose a given string and the need to compute some summaries on it, like the number of uppercase, lowercase, invalid chars and how many digits are present on that string.

Applying a reduce operation on each needed summary operation would result in more than one pass through the data, like this (here I am using the [var](https://developer.oracle.com/java/jdk-10-local-variable-type-inference.html) keyword introduced in [Java 10](https://www.oracle.com/java/technologies/java-archive-javase10-downloads.html)):

<script src="https://gist.github.com/rnaufal/ea6d58f6a609305e3835f2d9cf2fade7.js"></script>In the above code excerpt we are iterating three times through the string to compute the summaries. If we want to iterate just one time on the give string and get the desired results, we could fallback to the traditional imperative approach:

<script src="https://gist.github.com/rnaufal/69202d997e61dea7fead4d23a1ad299c.js"></script>Despite the solution above, there is another one: writing your own custom stream collector. This custom collector can compute the number of uppercase, lowercase, invalid chars and how many digits are present on the given string, in a single pass through the data. It is possible to make it run in `parallel` with the [Streams](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/Stream.html) API as well.

The custom stream collector shown here uses the `<a href="https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#chars()">chars()</a>` method of the [String](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html) class which returns an [IntStream](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/IntStream.html). The `IntStream` class contains a `collect()` method that computes a mutable reduction on the elements and returns its result in a container class.

The next example shows the container class code. It receives and accumulates each `char` of the String in the `accept()` method, thus categorizing it as a digit, uppercase char, lowercase char or as an invalid char.

<script src="https://gist.github.com/rnaufal/cfaadb809840c2408297a9c44e948287.js"></script>The complete implementation of the [collect()](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/IntStream.html#collect(java.util.function.Supplier,java.util.function.ObjIntConsumer,java.util.function.BiConsumer)) method which produces the result of the reduction in the [CharSummaryStatistics](https://github.com/rnaufal/blog/blob/master/summaries/src/main/java/br/com/rnaufal/summaries/CharSummaryStatistics.java) class is shown below. As a new char arrives, it is categorized in the `CharSummaryStatistics.accept()` method. The `CharSummaryStatistics.combine()` method is used to merge partial results.

<script src="https://gist.github.com/rnaufal/008e3fe2b338006c3ca2bce0025f76f7.js"></script>Have you ever written a custom Java stream collector? Please drop your comments here.

The complete source code can be found on [GitHub](https://github.com/rnaufal/blog/tree/master/summaries).

As a reference for writing this post, this [article](https://developer.ibm.com/articles/j-java-streams-2-brian-goetz/) is part of a series about [Streams](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/stream/Stream.html) and it is a good reference for learning how to aggregate and collect with Streams. All the articles from this series about Streams can be found [here](https://developer.ibm.com/series/java-streams/).