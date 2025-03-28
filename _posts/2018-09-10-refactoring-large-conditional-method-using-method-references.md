---
id: 673
title: 'Refactoring large conditional method using method references'
date: '2018-09-10T17:51:03-03:00'
author: rnaufal
layout: single
guid: 'https://rafaelnaufal.com/blog/?p=673'
categories:
    - code
    - development
    - functional
    - interface
    - java
    - java8
    - jdk8
    - lambdas
    - optional
    - polymorphism
    - programming
    - streams
tags:
    - code
    - development
    - functional
    - interface
    - java
    - java8
    - jdk8
    - lambdas
    - optional
    - polymorphism
    - programming
    - streams
---

Some years ago I wrote [junit-parameters](https://github.com/rnaufal/junit-parameters/), which is basically a custom JUnit test runner that make it possible to add parameters to [JUnit 4](https://junit.org/junit4) test methods.

Browsing its source code [SonarLint](https://www.sonarlint.org/intellij/) pointed me a large conditional `if/else` method from the `ParameterTypeConverterFactory` class:

<script src="https://gist.github.com/rnaufal/f6ce25027520bdead5cee88f9db4382f.js"></script>

This method converts the method parameter to its specific type based on its `Class` object. As it is few lines long, it showed me a good opportunity to refactor this code a little bit with a more elegant solution. This project has unit tests, so I could start refactoring it in [small steps](http://wiki.c2.com/?RefactoringInVerySmallSteps) and start over again whether I have made a mistake.

I started by defining a [functional interface](https://docs.oracle.com/javase/8/docs/api/java/lang/FunctionalInterface.html) called `ParameterConverter`:

<script src="https://gist.github.com/rnaufal/230a60294320d8f906cf9a7d99201fe1.js"></script>

and I created an [immutable map](https://google.github.io/guava/releases/23.0/api/docs/com/google/common/collect/ImmutableMap.html) which maps each `Class` object to its associated `ParameterConverter` instance (making use of [method references](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html)):

<script src="https://gist.github.com/rnaufal/1fcb73dcc5c731847571bae35ff0bf56.js"></script>

Then I refactored the original conditional method to get the `ParameterConverter` instance from the `convertersByClass` map and mapping to an `Optional` instance in case it didn’t exist.

After those refactorings, [SonarLint](https://www.sonarlint.org/intellij/) stopped warning me. Below is the modified version of the original method with some helper methods:

<script src="https://gist.github.com/rnaufal/2838c035c9cf4d36bd800a89d4024ec0.js"></script>

The complete code can be found at my GitHub [here](https://github.com/rnaufal/junit-parameters/blob/master/src/main/java/br/com/rnaufal/junit/parameters/statement/ParameterTypeConverterFactory.java).

This was the first change of breaking this complicated conditional method into a more readable one. It was safe to do so because after each change I could run my unit tests suite to assert I haven’t broken anything. The next refactoring could be towards a more object-oriented approach like [Replace Conditional with Polymorphism](https://refactoring.com/catalog/replaceConditionalWithPolymorphism.html).

What did you think about this refactoring? Have you ever had such a situation? Drop your comments here!