---
author: admin
comments: true
date: 2007-05-17 23:30:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2007/05/17/inspect-your-java-codebase-with-semmlecode/
slug: inspect-your-java-codebase-with-semmlecode
title: Inspect your Java codebase with SemmleCode
wordpress_id: 40
tags:
- java_programming
---

This [Eclipse](http://www.eclipse.org/) plugin seems to be a nice tool to drill down into your company codebase. You can gather with it code conventions, metrics, styles, method name patterns, all of it using a simple object-oriented query language, classe [.QL](http://semmle.com/product/ql).

This is a short description of what SemmleCode can do gor you to manage your code conventions (from [TheServerSide](http://www.theserverside.com/news/thread.tss?thread_id=45262)):



<blockquote>_[SemmleCode](http://semmle.com/product/SemmleCode)_ works by storing Eclipse projects in a relational database. You can then run queries to compute metrics, to find defects, to check style rules, and to navigate. For almost any frequent task, whether it involves a quality audit or a change impact analysis, there is a ready-made query that you can launch via the _run_ menu of Eclipse. In particular there are queries for Robert C. Martin's package metrics, and for checking J2EE coding conventions.</blockquote>



And about .QL:



<blockquote>[_.QL_](http://semmle.com/product/ql) is a simple object-oriented query language for writing queries over the codebase. It is very intuitive, andtightly integrated in Eclipse with syntax highlighting, auto-completion, and continuous checking. _.QL_ supports overriding of methods, and that is often very convenient for tailoring checks or metrics to a particular application. _SemmleCode_ puts you in the driving seat when it comes to quality audits: when youthink of a new check, it usually takes only a few lines of _.QL_ to implement it, and share it with other team members.</blockquote>



The plugin suggests us it can be a good tool to analyze our code conventions. I haven't tried it out yet (I'll share my thougths here when I do that :-) ), if you do, post your comments here.
