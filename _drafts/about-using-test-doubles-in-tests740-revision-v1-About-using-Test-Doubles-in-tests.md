---
id: 749
title: 'About using Test Doubles in tests'
date: '2024-03-08T17:14:07-03:00'
author: rnaufal
layout: revision
guid: 'https://rafaelnaufal.com/?p=749'
---

I have just read an interesting chapter from the [Software Engineering book at Google](https://abseil.io/resources/swe-book/html/toc.html) about using [Test Doubles](https://abseil.io/resources/swe-book/html/ch13.html) in tests.

The chapter discuss the various techniques of using test doubles in tests along with the pros and cons of using real implementations, fakes, stubbing with the support of mocking frameworks and interaction testing. It also refers to the benefits of running [Contract Tests](https://martinfowler.com/bliki/ContractTest.html) against the API’s public interface to catch contract changes prior to the production environment.

In my opinion, it is worth reading it to be aware of good practices when writing unit tests. Drop your comments here about what you think about it.