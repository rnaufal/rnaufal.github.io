---
id: 39
title: 'Method Refactoring'
date: '2007-04-15T22:52:00-03:00'
guid: 'http://rnaufal.wordpress.com/2007/04/15/method-refactoring/'
lj_itemid:
    - '45'
lj_permalink:
    - 'http://rnaufal.livejournal.com/11639.html'
dsq_thread_id:
    - '103076866'
categories:
    - Uncategorized
tags:
    - programming
---

[![[info]](http://stat.livejournal.com/img/userinfo.gif)](http://bpfurtado.livejournal.com/profile)[bpfurtado](http://bpfurtado.livejournal.com/39630.html) has raised an important question concerning some odd practices in software programming. People who code applying the same paradigm to all computer languages, thinking the only difference between programming languages are all about their syntax and grammar. These kind of code generate a lot of bad consequences, like the one I will focus at this post.

Sometimes I see people writing methods like “doX&amp;Y&amp;Z”, reflecting more than one responsability inside a method. Clearly this kind of design isn’t focused on reuse and maintenance, because people who code this way don’t even know such practices, characterized in OO programming. Methods must be cohesive, that is, “a cohesive method is responsible for one and only one well-defined logical task”.

Such a method could be factored into three little private methods, named “doX”, “doY” and “doZ”. To one public method is given the responsability to coordinate the tasks between the three methods. Talking about the former approach, how can you reuse one of the computation inside the “big” method? It’s impossible. So, reuse and maintenability is better achieved in the latter approach.

It occurs that people start programming in a language without knowing the [paradigm](http://en.wikipedia.org/wiki/Paradigm) it applies. So, people need to change their mind to produce better code, otherwise real big projects will continue to suffer the same problems we are tired of hearing nowadays.