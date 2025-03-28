---
id: 24
title: 'Single Responsability Principle'
date: '2006-08-15T23:06:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2006/08/15/single-responsability-principle/'
lj_itemid:
    - '21'
lj_permalink:
    - 'http://rnaufal.livejournal.com/5477.html'
dsq_thread_id:
    - '76181466'
categories:
    - Uncategorized
tags:
    - ooad
---

Look at these [Java](http://java.sun.com) code snippet:

```
<span class="gutter">   1:</span><span class="syntax9">import</span> java.util.Date;
<span class="gutter">   2:</span>
<span class="gutter">   3:</span><span class="syntax10">class</span> Movie
<span class="gutter">   4:</span><span class="syntax18">{</span>
<span class="gutterH">   5:</span>    <span class="syntax8">private</span> Date exhibitionDate;
<span class="gutter">   6:</span>    <span class="syntax8">private</span> Director director;
<span class="gutter">   7:</span>    <span class="syntax8">private</span> Persister persister <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax6">Persister</span>();
<span class="gutter">   8:</span>
<span class="gutter">   9:</span>    <span class="syntax8">public</span> <span class="syntax10">boolean</span> <span class="syntax6">isDirectedBy</span>(String director)
<span class="gutterH">  10:</span>    <span class="syntax18">{</span>
<span class="gutter">  11:</span>        <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">some</span><span class="syntax2"> </span><span class="syntax2">code</span><span class="syntax2"> </span><span class="syntax2">here;</span>
<span class="gutter">  12:</span>    <span class="syntax18">}</span>
<span class="gutter">  13:</span>
<span class="gutter">  14:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">changeDateWithDirectorApproval</span>(Date newDate)
<span class="gutterH">  15:</span>    <span class="syntax18">{</span>
<span class="gutter">  16:</span>        <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">some</span><span class="syntax2"> </span><span class="syntax2">code</span><span class="syntax2"> </span><span class="syntax2">here;</span>
<span class="gutter">  17:</span>    <span class="syntax18">}</span>
<span class="gutter">  18:</span>
<span class="gutter">  19:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">save</span>()
<span class="gutterH">  20:</span>    <span class="syntax18">{</span>
<span class="gutter">  21:</span>        persister.<span class="syntax6">save</span>(<span class="syntax14">this</span>);
<span class="gutter">  22:</span>    <span class="syntax18">}</span>
<span class="gutter">  23:</span><span class="syntax18">}</span>
```

At the *save()* method, *persister* takes care of the responsability to update the current movie, saving it at the persistent environment (a file, a DBMS, any data source, etc..) . Some may argue this class has two responsabilities: the Movie is responsible for its own behaviour AND its persistence. [ButUncleBob](http://butunclebob.com/ArticleS.DavidChelimsky.MattersOfPrinciple.SrpIsAboutImplementation) has an interesting opinion about the *Single Responsability Principle (SRP)*. It says *Movie* actually is not implementing persistence, the persister is a collaborator of the class. The persister is hidden from the client of the class, that is, is not part of the public interface. So, the lose coupling and the encapsulation is preserved. If the persister changes, the clients won’t be affected. It concludes *SRP is about implementation, not interface*. But imagine if you wanna find a movie, you can’t do movie.find() 🙂 . So, you have to deal with another collaborator who knows how to find a movie. Couldn’t be the *Persister*? No, because this one is hidden from the clients and if you become it public, you would fail with the [information hiding](http://en.wikipedia.org/wiki/Information_hiding) principle. In this case, I think it’s better a [Finder](http://www.martinfowler.com/eaaCatalog/registry.html) object. And you?