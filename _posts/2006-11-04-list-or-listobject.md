---
id: 31
title: 'List<?> or List<Object> ?'
date: '2006-11-04T00:03:00-03:00'
guid: 'http://rnaufal.wordpress.com/2006/11/04/list-or-listobject/'
lj_itemid:
    - '37'
lj_permalink:
    - 'http://rnaufal.livejournal.com/9687.html'
categories:
    - Uncategorized
tags:
    - java
---

Java 1.5 introduced some new concepts at the Java language level. One of them is Generics, which you can make use mainly when creating type safe collections. This new concept facilitates the programmers’ life: being type safe, errors when working with collections can be caught at compile time (if you have a *List&lt;String&gt;*in hand, only Strings can be added to this list, neither Integers, Cats or Dogs ) and the programmer doesn’t have to cast when taking out an object of a collection. I was thus wondering whether there is any difference between *List&lt;?&gt;* and *List&lt;Object&gt;*. Let’s take a look at the following lines of Java code:

```
<span class="gutter">   1:</span><span class="syntax9">import</span> java.util.ArrayList;
<span class="gutter">   2:</span><span class="syntax9">import</span> java.util.List;
<span class="gutter">   3:</span>
<span class="gutter">   4:</span><span class="syntax8">public</span> <span class="syntax10">class</span> Music
<span class="gutterH">   5:</span><span class="syntax18">{</span>
<span class="gutter">   6:</span>    <span class="syntax8">abstract</span> <span class="syntax10">class</span> Instrument
<span class="gutter">   7:</span>    <span class="syntax18">{</span>
<span class="gutter">   8:</span>    <span class="syntax18">}</span>
<span class="gutter">   9:</span>
<span class="gutterH">  10:</span>    <span class="syntax10">class</span> Guitar
<span class="gutter">  11:</span>            <span class="syntax8">extends</span> Instrument
<span class="gutter">  12:</span>    <span class="syntax18">{</span>
<span class="gutter">  13:</span>    <span class="syntax18">}</span>
<span class="gutter">  14:</span>
<span class="gutterH">  15:</span>    <span class="syntax10">class</span> Flute
<span class="gutter">  16:</span>            <span class="syntax8">extends</span> Instrument
<span class="gutter">  17:</span>    <span class="syntax18">{</span>
<span class="gutter">  18:</span>    <span class="syntax18">}</span>
<span class="gutter">  19:</span>
<span class="gutterH">  20:</span>    <span class="syntax10">class</span> Drums
<span class="gutter">  21:</span>            <span class="syntax8">extends</span> Instrument
<span class="gutter">  22:</span>    <span class="syntax18">{</span>
<span class="gutter">  23:</span>    <span class="syntax18">}</span>
<span class="gutter">  24:</span>
<span class="gutterH">  25:</span>    <span class="syntax8">public</span> <span class="syntax8">static</span> <span class="syntax10">void</span> <span class="syntax6">main</span>(String [ ] args)
<span class="gutter">  26:</span>    <span class="syntax18">{</span>
<span class="gutter">  27:</span>        List<span class="syntax18"><</span>Instrument<span class="syntax18">></span> instruments <span class="syntax18">=</span>
<span class="gutter">  28:</span>            <span class="syntax8">new</span> ArrayList<span class="syntax18"><</span>Instrument<span class="syntax18">></span>();
<span class="gutter">  29:</span>        List<span class="syntax18"><</span>Guitar<span class="syntax18">></span> guitars <span class="syntax18">=</span> <span class="syntax8">new</span> ArrayList<span class="syntax18"><</span>Guitar<span class="syntax18">></span>();
<span class="gutterH">  30:</span>        List<span class="syntax18"><</span>Flute<span class="syntax18">></span> flutes <span class="syntax18">=</span> <span class="syntax8">new</span> ArrayList<span class="syntax18"><</span>Flute<span class="syntax18">></span>();
<span class="gutter">  31:</span>        List<span class="syntax18"><</span>Drums<span class="syntax18">></span> drums <span class="syntax18">=</span> <span class="syntax8">new</span> ArrayList<span class="syntax18"><</span>Drums<span class="syntax18">></span>();
<span class="gutter">  32:</span>        List<span class="syntax18"><</span>Integer<span class="syntax18">></span> integers <span class="syntax18">=</span> <span class="syntax8">new</span> ArrayList<span class="syntax18"><</span>Integer<span class="syntax18">></span>();
<span class="gutter">  33:</span>        List<span class="syntax18"><</span>Object<span class="syntax18">></span> objects <span class="syntax18">=</span> <span class="syntax8">new</span> ArrayList<span class="syntax18"><</span>Object<span class="syntax18">></span>();
<span class="gutter">  34:</span>        <span class="syntax6">check</span>(instruments);
<span class="gutterH">  35:</span>        <span class="syntax6">check</span>(guitars);
<span class="gutter">  36:</span>        <span class="syntax6">check</span>(flutes);
<span class="gutter">  37:</span>        <span class="syntax6">check</span>(drums);
<span class="gutter">  38:</span>        <span class="syntax6">check</span>(integers);
<span class="gutter">  39:</span>        <span class="syntax6">validate</span>(objects);
<span class="gutterH">  40:</span>        <span class="syntax6">validate</span>(drums);
<span class="gutter">  41:</span>    <span class="syntax18">}</span>
<span class="gutter">  42:</span>
<span class="gutter">  43:</span>    <span class="syntax8">private</span> <span class="syntax8">static</span> <span class="syntax10">void</span> <span class="syntax6">check</span>(List<span class="syntax18"><</span>?<span class="syntax18">></span> instruments)
<span class="gutter">  44:</span>    <span class="syntax18">{</span>
<span class="gutterH">  45:</span>    <span class="syntax18">}</span>
<span class="gutter">  46:</span>
<span class="gutter">  47:</span>    <span class="syntax8">private</span> <span class="syntax8">static</span> <span class="syntax10">void</span> validate
<span class="gutter">  48:</span>        (List<span class="syntax18"><</span>Object<span class="syntax18">></span> instruments)
<span class="gutter">  49:</span>    <span class="syntax18">{</span>
<span class="gutterH">  50:</span>    <span class="syntax18">}</span>
<span class="gutter">  51:</span><span class="syntax18">}</span>
```

If you try to execute the lines of code, you´ll note:

- *List&lt;?&gt;*, which is the wildcard &lt;?&gt; bounded type, also know as *List&lt;capture-of ?&gt;*, simply means “any type.” That is, it could be a List of &lt;Guitar&gt;, &lt;Flute&gt;,&lt;Drums&gt;, whatever. It also means that you cannot **ADD** anything to the list referred to as *List&lt;?&gt;*.
- *List&lt;Object&gt;* only accepts Object as an argument. Not Guitars, Drums, Flutes or Integers. If you have a method which the argument specifies *List&lt;Object&gt;*, this method can only take a *List&lt;Object&gt;*. The compiler allows you to add to the *List&lt;Object&gt;*, since you pass an Object as an argument.

So, there are differences between *List&lt;?&gt;* and *List&lt;Object&gt;*. The above code doesn´t **compile**, because an *List&lt;Drums&gt;* is being passed to a method which has a *List&lt;Object&gt;* as argument. But if you modify the method to this one:

```
<span class="gutter">   1:</span><span class="syntax8">private</span> <span class="syntax8">static</span> <span class="syntax10">void</span> validate
<span class="gutter">   2:</span>        (List<span class="syntax18"><</span>? <span class="syntax8">extends</span> Object<span class="syntax18">></span> instruments)
<span class="gutter">   3:</span><span class="syntax18">{</span>
<span class="gutter">   4:</span><span class="syntax18">}</span>
```

The code now **compiles**!! So, we saw the behavior of *List&lt;?&gt;* and *List&lt;? extends Object&gt;* is the same! They both means “I can refer to any type of object”. But neither *List&lt;?&gt;* nor *List&lt;?&gt;* nor *List&lt;? extends Object&gt;* are the same as *List&lt;Object&gt;*. When you see code using the *wildcard notation (?)*, you can think: “this code refer to many options”. If you try to add something to a List&lt;?&gt;, the compiler won’t let you, because whether it were possible, it would be an unsafe operation, as you could pass a *List&lt;Guitar&gt;* to a method which receives a *List&lt;?&gt;* and add, say, a String to the list, as *List&lt;?&gt;* accepts “any type”. So now you may think: “Ok, Generics is a good feature, I can now create type safe collections and work with them in a safer way at compile time, that’s very good”. But everything isn’t the way we’d want it to be. If you try to mix Java generics code and legacy code,

```
<span class="gutter">   1:</span><span class="syntax8">private</span> <span class="syntax8">static</span> <span class="syntax10">void</span> <span class="syntax6">add</span>(List instruments)
<span class="gutter">   2:</span><span class="syntax18">{</span>
<span class="gutter">   3:</span>    instruments.<span class="syntax6">add</span>(<span class="syntax13">"</span><span class="syntax13">45</span><span class="syntax13">"</span>);
<span class="gutter">   4:</span><span class="syntax18">}</span>
```

and

```
<span class="gutter">   1:</span><span class="syntax6">add</span>(instruments);
<span class="gutter">   2:</span><span class="syntax6">add</span>(guitars);
<span class="gutter">   3:</span><span class="syntax6">add</span>(flutes);
<span class="gutter">   4:</span><span class="syntax6">add</span>(drums);
<span class="gutterH">   5:</span><span class="syntax6">add</span>(integers);
<span class="gutter">   6:</span><span class="syntax6">add</span>(objects);
```

It **compiles**!! But let’s deal with it in another post.