---
id: 743
title: 'Using Test Doubles in tests'
date: '2024-03-08T15:11:13-03:00'
author: rnaufal
layout: revision
guid: 'https://rafaelnaufal.com/?p=743'
---

I have just read an interesting chapter from the Software Engineering book at Google about using [Test Doubles](https://abseil.io/resources/swe-book/html/ch13.html) in tests.

The chapter discuss the various techniques of using test doubles along with the pros and cons of using real implementations, faking, stubbing with the support of mocking frameworks and interaction testing in tests. It also refers to the benefits of running [Contract Tests](https://martinfowler.com/bliki/ContractTest.html) against the API’s public interface to catch contract changes prior to the production environment.