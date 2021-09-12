---
author: admin
comments: true
date: 2010-05-09 19:56:23+00:00
layout: post
link: https://rafaelnaufal.com/blog/2010/05/09/eclipse-log4j-template/
slug: eclipse-log4j-template
title: Eclipse Log4J template
wordpress_id: 253
tags:
- eclipse
- java
- log4j
- logger
- templates
---

My friend [Bruno](http://bpfurtado.livejournal.com) sent me an interesting tip on how to create a [Log4J](http://logging.apache.org/log4j/) template at Eclipse. Just follow these steps:




	
  1. Go to _Window > Preferences > Java > Editor > Templates_

	
  2. Click _New_

	
  3. Write the string **logger** at the field _Name_ (this name will be used to call the template)

	
  4. At the field _Pattern_, write the following: 



<blockquote>private static final Logger LOGGER = Logger.getLogger(${enclosing_type}.class);
> 
> </blockquote>




	
	
  5. Click _OK_



The variable _${enclosing_type}_ refers to the enclosing type name. When you are ready, write down  **logger** on the field class declaration to have a logger added to the class.
