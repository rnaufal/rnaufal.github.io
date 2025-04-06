---
id: 42
title: 'Google Guice, dependence Inversion in the Java way'
date: '2007-06-03T19:02:00-03:00'
guid: 'http://rnaufal.wordpress.com/2007/06/03/google-guice-dependence-inversion-in-the-java-way/'
lj_itemid:
    - '48'
lj_permalink:
    - 'http://rnaufal.livejournal.com/12493.html'
dsq_thread_id:
    - '103328562'
categories:
    - Uncategorized
tags:
    - dip
    - framework
    - google
---

Check out this great [video](http://video.google.com/videoplay?docid=6068447410873108038&q=user%3A%22Google+engEDU) about the new Java based inversion control framework from [Google](http://www.google.com). The guys Kevin Bourillion and Bob Lee explains the concept behind dependency inversion principle ([dip](http://en.wikipedia.org/wiki/Dependency_injection)) and the core features inside Google Guice, called ‘juice’. The framework embraces and uses annotations instead of string identifiers (heavily used in [Spring](http://www.springframework.org/)) to inject dependencies into the code. The most interesting feature is that Guice <span style="background-color:yellow;font-weight:bold;font-size:120%;">injects constructors, fields and methods (any methods with any number of arguments, not just setters) </span>. You can also integrate Spring with Guice. Enjoy!