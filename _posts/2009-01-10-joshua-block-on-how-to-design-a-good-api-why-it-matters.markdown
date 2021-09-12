---
author: admin
comments: true
date: 2009-01-10 21:36:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2009/01/10/joshua-block-on-how-to-design-a-good-api-why-it-matters/
slug: joshua-block-on-how-to-design-a-good-api-why-it-matters
title: Joshua Block on How to Design a Good API & Why it Matters
wordpress_id: 67
tags:
- api
- google
- java
- joshua block
- programming
---

In this [talk](http://www.infoq.com/presentations/effective-api-design) (recorded at [Javapolis](http://www.javapolis.com/confluence/display/JP08/Home)), Joshua Block presents guidelines about how to design good APIs. I highlighted what i think are the most important parts of the talk:



  * Functionality should be easy to explain: If it's hard to name, that's generally a bad sign
  * Good names drive development
  * Be amenable to splitting and merging modules (If names are nasty, take a step back and make things easy to describe)
  * When in doubt, leave it out
  * You can always add, but tou cannot take it out
  * Implementation Should Not Impact API
  * Always omit implementation details
  * Inhibit freedom to change implementation
  * Don't let implementation details "leak" into API (For example: Serializable, hash functions)
  * Minimize Accessibility of Everything (This maximizes information hiding)
  * Public classes should'nt have public fields
  * API should be easy to learn, read and use: It should be consistent, it's a little language
  * Documentation matters (Example: Method contract between it and it's clients)
  * Think of preconditions, postconditions, side-effects
  * Don't Transliterate API's
    * What's the problem it solves?
    * What shoud abstractions did it use?
  * Don't Make the Client Do Anything The Module Could do
  * Throw Exceptions to Indicate Exceptional Conditions


When you see the talk, post your comments here.
