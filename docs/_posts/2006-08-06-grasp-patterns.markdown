---
author: admin
comments: true
date: 2006-08-06 17:05:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/08/06/grasp-patterns/
slug: grasp-patterns
title: GRASP patterns
wordpress_id: 22
tags:
- design
---

Have you ever been told about GRASP patterns? Those kind of patterns are part of the design discipline of the unified process.  Their goal is to assign classes responsabilities around the system. We can say GRASP patterns help objects and theirs collaborators to apply the correct behavior as well. I think the most important GRASP patterns are:


  * _Specialist_: put the responsability in the class with the specific knowledge. For instance, in a monetary system, as the account has the information of the balance value, the _withdraw()_ method has to be put in this class.

  


  * _Creator_: helps deciding who creates the object. If there is an association, aggregation or composition relationships, put in the composed object the responsability to create the other object.

  


  * _High Cohesion_: classes have only and exact one responsability around the system. Presentation classes don't have to know persistence classes. It's a measure of affinity and overloading responsabilities within classes. For instance, in the same monetary system, the Account class only _withdraw()_ money and not saves this information in a persistence mechanism, a collaborator can do this for the account object.

  


  * _Low coupling:_ measures classes dependencies within its context. Classes don't have to be very dependent on its context. For example, if I have to change my database design, I have to change my business objects also.

  


  * _Controller: _objects responsible to handle assynchronous event messages originated from GUI. Those can be the use case representation, a system or a subsystem, etcetera... They have the responsability to coordinate tasks and interactions between business objects.

Do you apply GRASP patterns on your software designs? To know more GRASP patterns, checkout [this](http://www.mindspring.com/~mgrand/pattern_synopses2.htm#GRASP%20Patterns).
