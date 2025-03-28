---
id: 40
title: 'Inspect your Java codebase with SemmleCode'
date: '2007-05-17T20:30:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2007/05/17/inspect-your-java-codebase-with-semmlecode/'
lj_itemid:
    - '46'
lj_permalink:
    - 'http://rnaufal.livejournal.com/11933.html'
dsq_thread_id:
    - '104522253'
categories:
    - Uncategorized
tags:
    - java_programming
---

This [Eclipse](http://www.eclipse.org/) plugin seems to be a nice tool to drill down into your company codebase. You can gather with it code conventions, metrics, styles, method name patterns, all of it using a simple object-oriented query language, classe [.QL](http://semmle.com/product/ql).

This is a short description of what SemmleCode can do gor you to manage your code conventions (from [TheServerSide](http://www.theserverside.com/news/thread.tss?thread_id=45262)):

> *[SemmleCode](http://semmle.com/product/SemmleCode)* works by storing Eclipse projects in a relational database. You can then run queries to compute metrics, to find defects, to check style rules, and to navigate. For almost any frequent task, whether it involves a quality audit or a change impact analysis, there is a ready-made query that you can launch via the *run* menu of Eclipse. In particular there are queries for Robert C. Martin’s package metrics, and for checking J2EE coding conventions.

And about .QL:

> [*.QL*](http://semmle.com/product/ql) is a simple object-oriented query language for writing queries over the codebase. It is very intuitive, andtightly integrated in Eclipse with syntax highlighting, auto-completion, and continuous checking. *.QL* supports overriding of methods, and that is often very convenient for tailoring checks or metrics to a particular application. *SemmleCode* puts you in the driving seat when it comes to quality audits: when youthink of a new check, it usually takes only a few lines of *.QL* to implement it, and share it with other team members.

The plugin suggests us it can be a good tool to analyze our code conventions. I haven’t tried it out yet (I’ll share my thougths here when I do that 🙂 ), if you do, post your comments here.