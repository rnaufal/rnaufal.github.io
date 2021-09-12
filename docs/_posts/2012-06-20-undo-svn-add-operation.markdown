---
author: admin
comments: true
date: 2012-06-20 17:09:02+00:00
layout: post
link: https://rafaelnaufal.com/blog/2012/06/20/undo-svn-add-operation/
slug: undo-svn-add-operation
title: Undo svn add operation
wordpress_id: 375
tags:
- add
- revert
- subversion
- svn
---

If you want to cancel an `svn add` operation, **do not use svn delete or svn remove**, according to this [post](http://data.agaric.com/undo-svn-add). You can issue the following command to undo a `svn add`:



<blockquote>svn revert --recursive your_folder
> 
> </blockquote>



This tip was very useful for me today :-)
