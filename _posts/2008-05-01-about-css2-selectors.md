---
id: 63
title: 'About CSS2 Selectors'
date: '2008-05-01T00:29:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2008/05/01/about-css2-selectors/'
lj_itemid:
    - '71'
lj_permalink:
    - 'http://rnaufal.livejournal.com/18287.html'
lj_current_mood:
    - sleepy
dsq_thread_id:
    - '103711817'
categories:
    - Uncategorized
tags:
    - css
    - html
    - web2.0
    - xhtml
---

Some days ago I was trying to customize my blog’s look and feel to remove my pic from each one of my entries.  
At my blog’s theme, every `<img>` tag (which contains my pic for each entry) is the first child of a `<td>` tag.  
I discovered a very handy [CSS2](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) selector syntax to accomplish this task:

> E:first-child: Matches element E when E is the firstchild of its parent ([The :first-child pseudo-class](http://www.w3.org/TR/REC-CSS2/selector.html#first-child))

So, the custom CSS ended up being `td > img:first-child {display: none;}`, which removes my user pic from every post, but keep the one on the left sidebar.

Just now you are seeing only one pic of mine 🙂