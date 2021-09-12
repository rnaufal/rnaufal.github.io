---
author: admin
comments: true
date: 2012-06-20 16:57:40+00:00
layout: post
link: https://rafaelnaufal.com/blog/2012/06/20/checkout-only-one-file-from-subversion/
slug: checkout-only-one-file-from-subversion
title: Checkout only one file from Subversion
wordpress_id: 368
tags:
- checkout
- client
- directory
- file
- svn
---

I was wondering how to checkout only one folder/file from SVN when I found this interesting [tip](http://stackoverflow.com/questions/122107/checkout-one-file-from-subversion). The command I issued to do it is the following:



<blockquote>svn co <url_of_big_dir> <target> --depth empty
> 
> </blockquote>



The above command checkout only one versioned directory, with its content empty. Now it's possible to add other files and directories under the directory who was checked out.
