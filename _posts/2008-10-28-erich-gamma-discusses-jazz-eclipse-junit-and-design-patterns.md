---
id: 66
title: 'Erich Gamma Discusses Jazz, Eclipse, JUnit and Design Patterns'
date: '2008-10-28T23:33:00-02:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2008/10/28/erich-gamma-discusses-jazz-eclipse-junit-and-design-patterns/'
lj_itemid:
    - '75'
lj_permalink:
    - 'http://rnaufal.livejournal.com/19237.html'
dsq_thread_id:
    - '102751363'
categories:
    - Uncategorized
tags:
    - design_patterns
    - dip
    - erich_gamma
    - infoq
    - junit
---

Good interview from [Erich Gamma](http://en.wikipedia.org/wiki/Erich_Gamma) at QCon London 2008, where he discusses, among other things, the JUnit framework, the Gang of Four book about [Design Patterns](http://en.wikipedia.org/wiki/Software_design_pattern) and the [Jazz](http://jazz.net/pub/index.jsp) project. I’ll try to summarize some of his interesting advices and responses here:

Why Eclipse is so successful:

> “We focus on stable APIs, so we understood it was a commitment up front and we maintained our APIs, so we tried to really avoid breaking our community..”

About [JUnit](http://www.junit.org/):

> “We always said it would just be as simple as writing System.out.println() but fully automated….I think the key was it makes writing tests as simple as writing this debug statement….”

About Design Patterns:

> “In Design Patterns we talked a lot about abstract coupling, that you can couple things by an abstract class, that the reference is only to an abstract class interface..”

> “Never use the class names we give in the pattern for it – that’s wrong. Use the domain-specific names, make it very specific to what your use..”

He also gives advices in how to identify design patterns:

- Something non-obvious
- The same kind of structure
- Confidence on multiple uses..

About [Dependency Injection](http://en.wikipedia.org/wiki/Dependency_injection):

> “I think it could be captured as a pattern. There are a lot of tradeoffs in there, it would fit into the whole creational realm..”

Check the whole presentation on [InfoQ here](http://www.infoq.com/interviews/gamma-jazz-eclipse-junit-design-patterns). It’s worthwhile to see.