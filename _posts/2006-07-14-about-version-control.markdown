---
author: admin
comments: true
date: 2006-07-14 02:38:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/07/13/about-version-control/
slug: about-version-control
title: About version control
wordpress_id: 19
tags:
- java
---

[What do java programmers version control? ](http://www.evolutionnext.com/blog/2006/07/07/1152287929432.html) is a good question to ask ourselves in the corporate world of software development. I think we should version control all the stuff regarding to the project knowledge, such as documents, wireframes, prototypes, notes, requeriments and obvious, source code :-). If you have a [wiki](http://en.wikipedia.org/wiki/Wiki) available, documents about the project can be put and edited there. I think the build process has to take care of creation and manipulation of other dependent libraries, they should not be versioned. At my company we use [Ivy](http://www.jayasoft.org/ivy), a java based dependency manager for this purpose. I haven't been told about this tool before but I found it quite interesting to work with dependencies. You can even specify which version of a specific jar you need, Ivy finds the correct version and applies it as a dependency to your project. It seems to be very useful to manage the dependencies of software projects. And in your company, what's your team allowed to version control?
