---
author: admin
comments: true
date: 2008-05-01 03:29:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2008/05/01/about-css2-selectors/
slug: about-css2-selectors
title: About CSS2 Selectors
wordpress_id: 63
tags:
- css
- html
- web2.0
- xhtml
---

Some days ago I was trying to customize my blog's look and feel to remove my pic from each one of my entries.
At my blog's theme, every `<img>` tag (which contains my pic for each entry) is the first child of a `<td>` tag.
I discovered a very handy [CSS2](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) selector syntax to accomplish this task:  

<blockquote>E:first-child: Matches element E when E is the firstchild of its parent ([The :first-child pseudo-class](http://www.w3.org/TR/REC-CSS2/selector.html#first-child))</blockquote>


So, the custom CSS ended up being `td > img:first-child {display: none;}`, which removes my user pic from every post, but keep the one on the left sidebar.

Just now you are seeing only one pic of mine :-)
