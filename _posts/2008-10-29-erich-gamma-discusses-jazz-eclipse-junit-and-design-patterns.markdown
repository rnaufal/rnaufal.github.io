---
author: admin
comments: true
date: 2008-10-29 02:33:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2008/10/28/erich-gamma-discusses-jazz-eclipse-junit-and-design-patterns/
slug: erich-gamma-discusses-jazz-eclipse-junit-and-design-patterns
title: Erich Gamma Discusses Jazz, Eclipse, JUnit and Design Patterns
wordpress_id: 66
tags:
- design_patterns
- dip
- erich_gamma
- infoq
- junit
---

Good interview from [Erich Gamma](http://en.wikipedia.org/wiki/Erich_Gamma) at QCon London 2008, where he discusses, among other things, the JUnit framework, the Gang of Four book about [Design Patterns](http://en.wikipedia.org/wiki/Software_design_pattern) and the [Jazz](http://jazz.net/pub/index.jsp) project. I'll try to summarize some of his interesting advices and responses here:

Why Eclipse is so successful:


<blockquote>"We focus on stable APIs, so we understood it was a commitment up front and we maintained our APIs, so we tried to really avoid breaking our community.."</blockquote>



About [JUnit](http://www.junit.org/):


<blockquote>"We always said it would just be as simple as writing System.out.println() but fully automated....I think the key was it makes writing tests as simple as writing this debug statement...."</blockquote>



About Design Patterns:


<blockquote>"In Design Patterns we talked a lot about abstract coupling, that you can couple things by an abstract class, that the reference is only to an abstract class interface.."</blockquote>




<blockquote>"Never use the class names we give in the pattern for it - that's wrong. Use the domain-specific names, make it very specific to what your use.."</blockquote>



He also gives advices in how to identify design patterns:



  * Something non-obvious
  * The same kind of structure
  * Confidence on multiple uses..


About [Dependency Injection](http://en.wikipedia.org/wiki/Dependency_injection):


<blockquote>"I think it could be captured as a pattern. There are a lot of tradeoffs in there, it would fit into the whole creational realm.."</blockquote>



Check the whole presentation on [InfoQ here](http://www.infoq.com/interviews/gamma-jazz-eclipse-junit-design-patterns). It's worthwhile to see.
