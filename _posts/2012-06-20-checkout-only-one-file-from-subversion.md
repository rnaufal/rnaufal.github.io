---
id: 368
title: 'Checkout only one file from Subversion'
guid: 'http://rafaelnaufal.com/blog/?p=368'
dsq_thread_id:
    - '749002135'
categories:
    - Uncategorized
tags:
    - checkout
    - client
    - directory
    - file
    - svn
---

I was wondering how to checkout only one folder/file from SVN when I found this interesting [tip](http://stackoverflow.com/questions/122107/checkout-one-file-from-subversion). The command I issued to do it is the following:

> svn co &lt;url\_of\_big\_dir&gt; &lt;target&gt; –depth empty

The above command checkout only one versioned directory, with its content empty. Now it’s possible to add other files and directories under the directory who was checked out.