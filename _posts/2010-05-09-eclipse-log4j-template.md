---
id: 253
title: 'Eclipse Log4J template'
guid: 'http://rafaelnaufal.com/blog/?p=253'
dsq_thread_id:
    - '102697806'
categories:
    - Uncategorized
tags:
    - eclipse
    - java
    - log4j
    - logger
    - templates
---

My friend [Bruno](http://bpfurtado.livejournal.com) sent me an interesting tip on how to create a [Log4J](http://logging.apache.org/log4j/) template at Eclipse. Just follow these steps:

1. Go to *Window &gt; Preferences &gt; Java &gt; Editor &gt; Templates*
2. Click *New*
3. Write the string **logger** at the field *Name* (this name will be used to call the template)
4. At the field *Pattern*, write the following:  
    > private static final Logger LOGGER = Logger.getLogger(${enclosing\_type}.class);
5. Click *OK*

The variable *${enclosing\_type}* refers to the enclosing type name. When you are ready, write down **logger** on the field class declaration to have a logger added to the class.