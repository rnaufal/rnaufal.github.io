---
id: 697
title: 'Jcombiner: Combinations of collections for Java'
date: '2018-11-27T22:49:10-02:00'
guid: 'https://rafaelnaufal.com/blog/?p=697'
medium_post:
    - 'O:11:"Medium_Post":11:{s:16:"author_image_url";s:74:"https://cdn-images-1.medium.com/fit/c/400/400/1*HWcHVsU9HX3OxkzLCFLyGQ.png";s:10:"author_url";s:27:"https://medium.com/@rnaufal";s:11:"byline_name";N;s:12:"byline_email";N;s:10:"cross_link";s:3:"yes";s:2:"id";s:12:"e6502c9cea57";s:21:"follower_notification";s:3:"yes";s:7:"license";s:19:"all-rights-reserved";s:14:"publication_id";s:2:"-1";s:6:"status";s:5:"draft";s:3:"url";s:40:"https://medium.com/@rnaufal/e6502c9cea57";}'
categories:
    - code
    - collections
    - collectors
    - combinations
    - development
    - functional
    - gradle
    - java
    - java11
    - jcombiner
    - jdk11
    - junit
    - junit5
    - lambdas
    - mockito
    - programming
    - streams
tags:
    - code
    - collections
    - collectors
    - combinations
    - development
    - functional
    - gradle
    - java
    - java11
    - jcombiner
    - jdk11
    - junit
    - junit5
    - lambdas
    - mockito
    - programming
    - streams
---

[JCombiner](https://github.com/rnaufal/jcombiner) is a framework to generate combinations of collections for Java. I have written it in [Java 11](https://openjdk.java.net/projects/jdk/11/) using Java 9 modules ([JPMS](https://openjdk.java.net/projects/jigsaw/quick-start)) and [Gradle](https://gradle.org/) as build tool. [JUnit 5](https://junit.org/junit5/) and [Mockito](https://site.mockito.org/) are used for unit testing and [Jacoco](https://www.eclemma.org/jacoco/) for code coverage. [Streams](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/Stream.html) and the [Collectors](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/Collectors.html) API are extensively used throughout the development of JCombiner project.

Jcombiner’s source code is available under [GitHub](https://github.com/rnaufal/jcombiner).

Code examples of its usage can be found on GitHub [here](https://github.com/rnaufal/jcombiner/blob/master/README.md#usage). More examples can be found on [this](https://github.com/rnaufal/jcombiner/tree/master/client) module inside JCombiner.

Share your comments about this framework here! Please feel free to [contribute](https://help.github.com/articles/creating-a-pull-request) to it, more features are welcome!