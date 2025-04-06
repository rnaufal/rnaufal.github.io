---
id: 146
title: 'Fixing Eclipse buttons for Ubuntu 9.10'
date: '2009-11-13T15:43:17-02:00'
guid: 'http://rafaelnaufal.com/blog/?p=146'
dsq_thread_id:
    - '76181492'
categories:
    - Uncategorized
tags:
    - buttons
    - eclipse
    - gtk
    - Karmic
    - koala
    - swt
    - Ubuntu9.10
---

I’ve just updated to the new Ubuntu Karmic 9.10 and I’ve found some weird problems running Eclipse. Some buttons didn’t work when they were clicked, but the keyboard shortcuts worked well. It looks like in Eclipse 3.6 the bug will be solved. It looks like it’s a hack between Eclipse SWT and GTK. More information [here](http://art.ubuntuforums.org/showthread.php?p=8293905), [here](https://bugs.launchpad.net/azureus/+bug/443004) and [here](http://www.eclipse.org/forums/index.php?t=msg&goto=494621&S=58353ef07becea1678a9a42bc12fe275).

To fix the problem, just launch Eclipse through this shell script file, assuming Eclipse is installed at **/home/rnaufal/eclipse/eclipse**:

> \#!/bin/sh  
> export GDK\_NATIVE\_WINDOWS=1  
> /home/rnaufal/eclipse/eclipse