---
id: 375
title: 'Undo svn add operation'
date: '2012-06-20T14:09:02-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=375'
dsq_thread_id:
    - '751435668'
categories:
    - Uncategorized
tags:
    - add
    - revert
    - subversion
    - svn
---

If you want to cancel an `svn add` operation, **do not use svn delete or svn remove**, according to this [post](http://data.agaric.com/undo-svn-add). You can issue the following command to undo a `svn add`:``

> svn revert --recursive your\_folder

This tip was very useful for me today :-)