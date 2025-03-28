---
id: 26
title: 'Applying the Law of Demeter'
date: '2006-09-11T00:01:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2006/09/11/applying-the-law-of-demeter/'
lj_itemid:
    - '32'
lj_permalink:
    - 'http://rnaufal.livejournal.com/8351.html'
dsq_thread_id:
    - '102853302'
categories:
    - Uncategorized
tags:
    - oop
---

Have you ever been told about the [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter) when developing object-oriented systems? This law states the following:

More formally, the Law of Demeter for functions requires that any method *M* of an object *O* may only invoke the methods of the following kinds of objects:

1. itself
2. its parameters
3. any objects it creates/instantiates
4. its direct component objects

In particular, an object should avoid invoking methods of a member object returned by another method.

Browsing the source code of a project, I found this Java code stretch:

```
<span class="gutter">   1:</span><span class="syntax8">public</span> <span class="syntax10">class</span> AccountHelper
<span class="gutter">   2:</span><span class="syntax18">{</span>
<span class="gutter">   3:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">creditToAccount</span>(Account account, <span class="syntax10">double</span> value)
<span class="gutter">   4:</span>    <span class="syntax18">{</span>
<span class="gutterH">   5:</span>        <span class="syntax10">double</span> balance <span class="syntax18">=</span> account.<span class="syntax6">balance</span>();
<span class="gutter">   6:</span>        <span class="syntax10">double</span> newBalance <span class="syntax18">=</span> balance <span class="syntax18">+</span> value;
<span class="gutter">   7:</span>        account.<span class="syntax6">setBalance</span>(newBalance);
<span class="gutter">   8:</span>    <span class="syntax18">}</span>
<span class="gutter">   9:</span>
<span class="gutterH">  10:</span>    <span class="syntax8">public</span> <span class="syntax10">boolean</span> <span class="syntax6">withdrawFromAccount</span>(Account account,
<span class="gutter">  11:</span>            <span class="syntax10">double</span> value)
<span class="gutter">  12:</span>    <span class="syntax18">{</span>
<span class="gutter">  13:</span>        <span class="syntax10">double</span> balance <span class="syntax18">=</span> account.<span class="syntax6">balance</span>();
<span class="gutter">  14:</span>        <span class="syntax10">double</span> limit <span class="syntax18">=</span> account.<span class="syntax6">limit</span>();
<span class="gutterH">  15:</span>        <span class="syntax10">double</span> newBalance <span class="syntax18">=</span> balance;
<span class="gutter">  16:</span>        <span class="syntax10">boolean</span> canWithdraw <span class="syntax18">=</span> <span class="syntax14">false</span>;
<span class="gutter">  17:</span>        <span class="syntax8">if</span>(balance <span class="syntax18">+</span> limit <span class="syntax18">>=</span> value) <span class="syntax18">{</span>
<span class="gutter">  18:</span>            newBalance <span class="syntax18">=</span> balance <span class="syntax18">-</span> value;
<span class="gutter">  19:</span>            canWithdraw <span class="syntax18">=</span> <span class="syntax14">true</span>;
<span class="gutterH">  20:</span>        <span class="syntax18">}</span>
<span class="gutter">  21:</span>        account.<span class="syntax6">setBalance</span>(newBalance);
<span class="gutter">  22:</span>        <span class="syntax8">return</span> canWithdraw;
<span class="gutter">  23:</span>    <span class="syntax18">}</span>
<span class="gutter">  24:</span><span class="syntax18">}</span>
```

This code snippet doesn’t follow demeter’s law. And it’s hiding a responsability that would have been better in the *Account* class. If the *Account* knows its balance and limit, why putting the credit and withdraw behavior in a helper class? If we follow the [**Specialist**](http://rnaufal.livejournal.com/#rnaufal4963) grasp pattern, the responsability has to be at the class with the specific knowledge. So, I’ve improved the design to this new one Java code:

```
<span class="gutter">   1:</span><span class="syntax9">import</span> java.math.BigDecimal;
<span class="gutter">   2:</span>
<span class="gutter">   3:</span><span class="syntax8">public</span> <span class="syntax10">class</span> Account
<span class="gutter">   4:</span><span class="syntax18">{</span>
<span class="gutterH">   5:</span>    <span class="syntax8">private</span> BigDecimal balance;
<span class="gutter">   6:</span>    <span class="syntax8">private</span> BigDecimal limit;
<span class="gutter">   7:</span>
<span class="gutter">   8:</span>    <span class="syntax8">public</span> <span class="syntax6">Account</span>(<span class="syntax10">double</span> balance)
<span class="gutter">   9:</span>    <span class="syntax18">{</span>
<span class="gutterH">  10:</span>        <span class="syntax14">this</span>.balance <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax6">BigDecimal</span>(balance);
<span class="gutter">  11:</span>    <span class="syntax18">}</span>
<span class="gutter">  12:</span>
<span class="gutter">  13:</span>    <span class="syntax8">public</span> <span class="syntax6">Account</span>(<span class="syntax10">double</span> amount,
<span class="gutter">  14:</span>        <span class="syntax10">double</span> limit)
<span class="gutterH">  15:</span>    <span class="syntax18">{</span>
<span class="gutter">  16:</span>        <span class="syntax14">this</span>(amount);
<span class="gutter">  17:</span>        <span class="syntax14">this</span>.limit <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax6">BigDecimal</span>(limit);
<span class="gutter">  18:</span>    <span class="syntax18">}</span>
<span class="gutter">  19:</span>
<span class="gutterH">  20:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">credit</span>(<span class="syntax10">double</span> value)
<span class="gutter">  21:</span>    <span class="syntax18">{</span>
<span class="gutter">  22:</span>        balance <span class="syntax18">=</span> balance.<span class="syntax6">add</span>(<span class="syntax8">new</span> <span class="syntax6">BigDecimal</span>(value));
<span class="gutter">  23:</span>    <span class="syntax18">}</span>
<span class="gutter">  24:</span>
<span class="gutterH">  25:</span>    <span class="syntax8">public</span> <span class="syntax10">boolean</span> <span class="syntax6">withdraw</span>(<span class="syntax10">double</span> quantity)
<span class="gutter">  26:</span>    <span class="syntax18">{</span>
<span class="gutter">  27:</span>        <span class="syntax8">if</span>(<span class="syntax6">canWithdraw</span>(quantity)) <span class="syntax18">{</span>
<span class="gutter">  28:</span>            balance.<span class="syntax6">subtract</span>(<span class="syntax8">new</span> <span class="syntax6">BigDecimal</span>(quantity));
<span class="gutter">  29:</span>            <span class="syntax8">return</span> <span class="syntax14">true</span>;
<span class="gutterH">  30:</span>        <span class="syntax18">}</span>
<span class="gutter">  31:</span>        <span class="syntax8">return</span> <span class="syntax14">false</span>;
<span class="gutter">  32:</span>    <span class="syntax18">}</span>
<span class="gutter">  33:</span>
<span class="gutter">  34:</span>    <span class="syntax8">public</span> <span class="syntax10">double</span> <span class="syntax6">balance</span>()
<span class="gutterH">  35:</span>    <span class="syntax18">{</span>
<span class="gutter">  36:</span>        <span class="syntax8">return</span> balance.<span class="syntax6">doubleValue</span>();
<span class="gutter">  37:</span>    <span class="syntax18">}</span>
<span class="gutter">  38:</span>
<span class="gutter">  39:</span>    <span class="syntax8">private</span> <span class="syntax10">boolean</span> <span class="syntax6">canWithdraw</span>(<span class="syntax10">double</span> quantity)
<span class="gutterH">  40:</span>    <span class="syntax18">{</span>
<span class="gutter">  41:</span>        <span class="
syntax8">return</span> (balance.<span class="syntax6">doubleValue</span>() <span class="syntax18">+</span> 
<span class="gutter">  42:</span>                limit.<span class="syntax6">doubleValue</span>() <span class="syntax18">>=</span> quantity)
<span class="gutter">  43:</span>                ? <span class="syntax14">true</span>
<span class="gutter">  44:</span>                : <span class="syntax14">false</span>;
<span class="gutterH">  45:</span>    <span class="syntax18">}</span>
<span class="gutter">  46:</span>
<span class="gutter">  47:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">setBalance</span>(<span class="syntax10">double</span> balance)
<span class="gutter">  48:</span>    <span class="syntax18">{</span>
<span class="gutter">  49:</span>        <span class="syntax14">this</span>.balance <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax6">BigDecimal</span>(balance);
<span class="gutterH">  50:</span>    <span class="syntax18">}</span>
<span class="gutter">  51:</span>
<span class="gutter">  52:</span>    <span class="syntax8">public</span> <span class="syntax10">double</span> <span class="syntax6">limit</span>()
<span class="gutter">  53:</span>    <span class="syntax18">{</span>
<span class="gutter">  54:</span>        <span class="syntax8">return</span> limit.<span class="syntax6">doubleValue</span>();
<span class="gutterH">  55:</span>    <span class="syntax18">}</span>
<span class="gutter">  56:</span><span class="syntax18">}</span>
```

So, the initial Java code stretch become this one:

```
<span class="gutter">   1:</span><span class="syntax8">public</span> <span class="syntax10">class</span> AccountHelper
<span class="gutter">   2:</span><span class="syntax18">{</span>
<span class="gutter">   3:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">credit</span>(Account account, <span class="syntax10">double</span> value)
<span class="gutter">   4:</span>    <span class="syntax18">{</span>
<span class="gutterH">   5:</span>        <span class="syntax6">assert</span> account <span class="syntax18">!</span><span class="syntax18">=</span> <span class="syntax14">null</span>;
<span class="gutter">   6:</span>        account.<span class="syntax6">credit</span>(value);
<span class="gutter">   7:</span>    <span class="syntax18">}</span>
<span class="gutter">   8:</span>
<span class="gutter">   9:</span>    <span class="syntax8">public</span> <span class="syntax10">boolean</span> <span class="syntax6">withdraw</span>(Account account, <span class="syntax10">double</span> value)
<span class="gutterH">  10:</span>    <span class="syntax18">{</span>
<span class="gutter">  11:</span>        <span class="syntax6">assert</span> account <span class="syntax18">!</span><span class="syntax18">=</span> <span class="syntax14">null</span>;
<span class="gutter">  12:</span>        <span class="syntax8">return</span> account.<span class="syntax6">withdraw</span>(value);
<span class="gutter">  13:</span>    <span class="syntax18">}</span>
<span class="gutter">  14:</span><span class="syntax18">}</span>
```

This code above is better because we hide from the clients the *Account* class internal structure (clients don’t need to know the existence of suborders). Moreover, if the internal structure of account is intended to change, less clients would suffer with those changes (actually, if the Account class changes, only it would have to receive the changes and its clients would have to stay far away from its changes. It’s why Object Oriented design is focused in **behavior** instead of **state**). This nice phrase resumes demeter’s law: *“The resulting software tends to be more maintainable and adaptable. Since objects are less dependent on the internal structure of other objects, object containers can be changed without reworking their callers”*.