---
id: 218
title: 'Using Hamcrest and JUnit'
date: '2010-03-15T23:10:52-03:00'
author: rnaufal
layout: single
guid: 'http://rafaelnaufal.com/blog/?p=218'
dsq_thread_id:
    - '76180944'
categories:
    - Uncategorized
tags:
    - google
    - hamcrest
    - java
    - junit
    - matchers
    - testing
    - tests
---

Lately I started using the core [Hamcrest](http://junit.sourceforge.net/doc/ReleaseNotes4.4.html) matchers bundled with the JUnit framework to create more readable unit tests.

Hamcrest matchers were created to improve the readability of unit testing code. It’s a framework which facilitates the creation of *matcher* objects to match rules specified in unit tests. Some examples will let it to be clearer:

```
<span class="syntax0"><span class="gutter">   1 </span><span class="syntax-KEYWORD2">import</span> <span class="syntax-KEYWORD1">static</span> org.hamcrest.CoreMatchers.equalTo;
<span class="gutter">   2 </span><span class="syntax-KEYWORD2">import</span> <span class="syntax-KEYWORD1">static</span> org.hamcrest.CoreMatchers.is;
<span class="gutter">   3 </span><span class="syntax-KEYWORD2">import</span> <span class="syntax-KEYWORD1">static</span> org.junit.Assert.assertThat;
<span class="gutter">   4 </span>
<span class="gutterH">   5 </span><span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Test</span>
<span class="gutter">   6 </span><span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">void</span> <span class="syntax-FUNCTION">shouldBeTheSamePerson</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span>
<span class="gutter">   7 </span><span class="syntax-OPERATOR">{</span>
<span class="gutter">   8 </span>    Person me <span class="syntax-OPERATOR">=</span> <span class="syntax-KEYWORD1">new</span> <span class="syntax-FUNCTION">Person</span><span class="syntax-OPERATOR">(</span> <span class="syntax-LITERAL1">"</span><span class="syntax-LITERAL1">Rafael</span><span class="syntax-LITERAL1">"</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">   9 </span>    Person theOther <span class="syntax-OPERATOR">=</span> <span class="syntax-KEYWORD1">new</span> <span class="syntax-FUNCTION">Person</span><span class="syntax-OPERATOR">(</span> <span class="syntax-LITERAL1">"</span><span class="syntax-LITERAL1">Rafael</span><span class="syntax-LITERAL1">"</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutterH">  10 </span>    <span class="syntax-FUNCTION">assertThat</span><span class="syntax-OPERATOR">(</span> me, <span class="syntax-FUNCTION">is</span><span class="syntax-OPERATOR">(</span> theOther <span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">  11 </span><span class="syntax-OPERATOR">}</span>
<span class="gutter">  12 </span>
<span class="gutter">  13 </span><span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Test</span>
<span class="gutter">  14 </span><span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">void</span> <span class="syntax-FUNCTION">shouldHaveFixedSizeNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span>
<span class="gutterH">  15 </span><span class="syntax-OPERATOR">{</span>
<span class="gutter">  16 </span>    List<span class="syntax-OPERATOR"><</span>Integer<span class="syntax-OPERATOR">></span> numbers <span class="syntax-OPERATOR">=</span> Arrays.<span class="syntax-FUNCTION">asList</span><span class="syntax-OPERATOR">(</span> <span class="syntax-DIGIT">1</span>, <span class="syntax-DIGIT">2</span>, <span class="syntax-DIGIT">3</span>, <span class="syntax-DIGIT">4</span>, <span class="syntax-DIGIT">5</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">  17 </span>    <span class="syntax-FUNCTION">assertThat</span><span class="syntax-OPERATOR">(</span> numbers.<span class="syntax-FUNCTION">size</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span>, <span class="syntax-FUNCTION">is</span><span class="syntax-OPERATOR">(</span> <span class="syntax-FUNCTION">equalTo</span><span class="syntax-OPERATOR">(</span> <span class="syntax-DIGIT">5</span> <span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">  18 </span><span class="syntax-OPERATOR">}</span>
</span>
```

The first example checks if one `Person` object is equal to another using the `Object equals `method, which was overridden in the `Person` class. The `is` syntax defines a matcher which is a shorthand to `is(equalTo(value))`. The second one uses the `is(equalTo(value))` matcher to check the size of an integer list of fixed size numbers. The `assertThat` method is used in conjunction with the `is(equalTo(value))` matcher, which makes the test sentence very human readable.

An interesting thing is the possibility to create a custom matcher, like this one which tests if a given list only has even numbers:

```
<span class="syntax0"><span class="gutter">   1 </span><span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">class</span> AreEvenNumbers <span class="syntax-KEYWORD1">extends</span> TypeSafeMatcher<span class="syntax-OPERATOR"><</span>Collection<span class="syntax-OPERATOR"><</span>Integer<span class="syntax-OPERATOR">></span><span class="syntax-OPERATOR">></span> <span class="syntax-OPERATOR">{</span>
<span class="gutter">   2 </span>
<span class="gutter">   3 </span>    <span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Override</span>
<span class="gutter">   4 </span>    <span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">boolean</span> <span class="syntax-FUNCTION">matchesSafely</span><span class="syntax-OPERATOR">(</span>Collection<span class="syntax-OPERATOR"><</span>Integer<span class="syntax-OPERATOR">></span> numbers<span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">{</span>
<span class="gutterH">   5 </span>        <span class="syntax-KEYWORD1">for</span> <span class="syntax-OPERATOR">(</span>Integer number : numbers<span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">{</span>
<span class="gutter">   6 </span>            <span class="syntax-KEYWORD1">if</span> <span class="syntax-OPERATOR">(</span>number <span class="syntax-OPERATOR">%</span> <span class="syntax-DIGIT">2</span> <span class="syntax-OPERATOR">!</span><span class="syntax-OPERATOR">=</span> <span class="syntax-DIGIT">0</span><span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">{</span>
<span class="gutter">   7 </span>                <span class="syntax-KEYWORD1">return</span> <span class="syntax-LITERAL2">false</span>;
<span class="gutter">   8 </span>            <span class="syntax-OPERATOR">}</span>
<span class="gutter">   9 </span>        <span class="syntax-OPERATOR">}</span>
<span class="gutterH">  10 </span>        <span class="syntax-KEYWORD1">return</span> <span class="syntax-LITERAL2">true</span>;
<span class="gutter">  11 </span>    <span class="syntax-OPERATOR">}</span>
<span class="gutter">  12 </span>
<span class="gutter">  13 </span>    <span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Override</span>
<span class="gutter">  14 </span>    <span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">void</span> <span class="syntax-FUNCTION">describeTo</span><span class="syntax-OPERATOR">(</span>Description description<span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">{</span>
<span class="gutterH">  15 </span>        description.<span class="syntax-FUNCTION">appendText</span><span class="syntax-OPERATOR">(</span><span class="syntax-LITERAL1">"</span><span class="syntax-LITERAL1">even</span><span class="syntax-LITERAL1"> </span><span class="syntax-LITERAL1">numbers</span><span class="syntax-LITERAL1">"</span><span class="syntax-OPERATOR">)</span>;
<span class="gutter">  16 </span>    <span class="syntax-OPERATOR">}</span>
<span class="gutter">  17 </span>
<span class="gutter">  18 </span>    <span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Factory</span>
<span class="gutter">  19 </span>    <span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD1">static</span> <span class="syntax-OPERATOR"><</span>T<span class="syntax-OPERATOR">></span> Matcher<span class="syntax-OPERATOR"><</span>Collection<span class="syntax-OPERATOR"><</span>Integer<span class="syntax-OPERATOR">></span><span class="syntax-OPERATOR">></span> <span class="syntax-FUNCTION">evenNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">{</span>
<span class="gutterH">  20 </span>        <span class="syntax-KEYWORD1">return</span> <span class="syntax-KEYWORD1">new</span> <span class="syntax-FUNCTION">AreEvenNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span>;
<span class="gutter">  21 </span>    <span class="syntax-OPERATOR">}</span>
<span class="gutter">  22 </span><span class="syntax-OPERATOR">}</span>
</span>
```

And below are two tests which uses the `AreEvenNumbers` custom matcher:

```
<span class="syntax0"><span class="gutter">   1 </span><span class="syntax-KEYWORD2">import</span> <span class="syntax-KEYWORD1">static</span> org.hamcrest.CoreMatchers.is;
<span class="gutter">   2 </span><span class="syntax-KEYWORD2">import</span> <span class="syntax-KEYWORD1">static</span> org.junit.Assert.assertThat;
<span class="gutter">   3 </span><span class="syntax-KEYWORD2">import</span> <span class="syntax-KEYWORD1">static</span> br.com.rafael.hamcrest.AreEvenNumbers.evenNumbers;
<span class="gutter">   4 </span>
<span class="gutterH">   5 </span><span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Test</span>
<span class="gutter">   6 </span><span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">void</span> <span class="syntax-FUNCTION">shouldHaveOnlyEvenNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span>
<span class="gutter">   7 </span><span class="syntax-OPERATOR">{</span>
<span class="gutter">   8 </span>    List<span class="syntax-OPERATOR"><</span>Integer<span class="syntax-OPERATOR">></span> numbers <span class="syntax-OPERATOR">=</span> Arrays.<span class="syntax-FUNCTION">asList</span><span class="syntax-OPERATOR">(</span> <span class="syntax-DIGIT">2</span>, <span class="syntax-DIGIT">4</span>, <span class="syntax-DIGIT">6</span>, <span class="syntax-DIGIT">8</span>, <span class="syntax-DIGIT">10</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">   9 </span>    <span class="syntax-FUNCTION">assertThat</span><span class="syntax-OPERATOR">(</span> numbers, <span class="syntax-FUNCTION">is</span><span class="syntax-OPERATOR">(</span> <span class="syntax-FUNCTION">evenNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutterH">  10 </span><span class="syntax-OPERATOR">}</span>
<span class="gutter">  11 </span>
<span class="gutter">  12 </span><span class="syntax-KEYWORD4">@</span><span class="syntax-KEYWORD4">Test</span>
<span class="gutter">  13 </span><span class="syntax-KEYWORD1">public</span> <span class="syntax-KEYWORD3">void</span> <span class="syntax-FUNCTION">shouldNotHaveOddNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span>
<span class="gutter">  14 </span><span class="syntax-OPERATOR">{</span>
<span class="gutterH">  15 </span>    List<span class="syntax-OPERATOR"><</span>Integer<span class="syntax-OPERATOR">></span> numbers <span class="syntax-OPERATOR">=</span> Arrays.<span class="syntax-FUNCTION">asList</span><span class="syntax-OPERATOR">(</span> <span class="syntax-DIGIT">1</span>, <span class="syntax-DIGIT">2</span>, <span class="syntax-DIGIT">4</span>, <span class="syntax-DIGIT">6</span>, <span class="syntax-DIGIT">8</span>, <span class="syntax-DIGIT">10</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">  16 </span>    <span class="syntax-FUNCTION">assertThat</span><span class="syntax-OPERATOR">(</span> numbers, <span class="syntax-FUNCTION">not</span><span class="syntax-OPERATOR">(</span> <span class="syntax-FUNCTION">evenNumbers</span><span class="syntax-OPERATOR">(</span><span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span> <span class="syntax-OPERATOR">)</span>;
<span class="gutter">  17 </span><span class="syntax-OPERATOR">}</span>
</span>
```

These two tests use the static factory method `evenNumbers` to instantiate the matcher on the test code. Not the use of the `not` matcher on the `shouldNotHaveOddNumbers` test to assert that no odd numbers are present on the given list. All tests use the [static import](http://java.sun.com/j2se/1.5.0/docs/guide/language/static-import.html) feature, which turns the test not clean and not cluttered with the class qualification.

I haven’t experienced the other common matchers on unit testing code, like the Beans, Collections and Number ones. I think they turn the tests more readable, clean and easy to change. And you? Have you ever used Hamcrest matcher? If you have other examples of using it, post them here!

***Updated:** Static imports were added to the testing code.*