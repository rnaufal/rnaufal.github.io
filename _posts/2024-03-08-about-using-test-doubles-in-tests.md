---
id: 740
title: 'About using Test Doubles in tests'
date: '2024-03-08T15:52:10-03:00'
guid: 'https://rafaelnaufal.com/?p=740'
categories:
    - java
    - junit
    - mockito
    - programming
    - test
    - testing
    - tests
    - unittests
tags:
    - fakes
    - java
    - junit
    - mocking
    - mockito
    - programming
    - stubbing
    - testdoubles
    - testing
    - tests
    - unittests
---

I have just read an interesting chapter from the [Software Engineering book at Google](https://abseil.io/resources/swe-book/html/toc.html) about using [Test Doubles](https://abseil.io/resources/swe-book/html/ch13.html) in tests.

The chapter discuss the various techniques of using test doubles in tests along with the pros and cons of using real implementations, fakes, stubbing with the support of mocking frameworks and interaction testing. It also refers to the benefits of running [Contract Tests](https://martinfowler.com/bliki/ContractTest.html) against the API’s public interface to catch contract changes prior to the production environment.

In my opinion, it is worth reading it to be aware of good practices when writing unit tests. Drop your comments here about what you think about it.