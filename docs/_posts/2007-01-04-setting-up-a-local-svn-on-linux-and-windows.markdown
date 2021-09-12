---
author: admin
comments: true
date: 2007-01-04 02:19:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2007/01/03/setting-up-a-local-svn-on-linux-and-windows/
slug: setting-up-a-local-svn-on-linux-and-windows
title: Setting up a local SVN on Linux and Windows
wordpress_id: 35
tags:
- os_linux
---

I was intended to create a local [SVN](http://subversion.tigris.org/) repository to host my [Eclipse](http://www.eclipse.org/) projects in home. So, I decided to share the same SVN repository on Linux (a _[Kubuntu](http://www.kubuntu.org/) distro_) and Windows, to synchronize my projects in an easy manner. Here are the steps to get the things done:



  1. Create a [FAT32](http://en.wikipedia.org/wiki/File_Allocation_Table) partition to host your SVN repository. You cannot configure your local home repository in [NTFS](http://en.wikipedia.org/wiki/NTFS) file system type because Linux can't write at NTFS partitions.
  2. Create a SVN repository on Windows using the [Tortoise](http://tortoisesvn.tigris.org/) utility. This tool is free and makes the repository creation very easy. If you don't know Tortoise, take a look at the tutorial to be comfortable with the tool. You can create a local repository on any folder in your file system. It's just click the right button and select _TortoiseSVN -> Create repository here..._
  3. So now your repository is created on your local file system. Now you have to download and install Subclipse (if you don't have downloaded yet :-)), which is an Eclipse plugin to interact with SVN. 
  4. When you install [Subclipse](http://subclipse.tigris.org/), open your Eclipse platform and go to _Windows -> Preferences -> Team -> SVN_ and select _SVNKit (Pure Java)_. This interface allows you to interact with the repository installed on your local machine. 
  5. Now open the _SVN Repository Exploring perspective_, click the right button and select _New -> Repository Location_. In my machine my SVN repository is configured in other partition (remember this partition has to be FAT32).


The dialog box starts to ask you the SVN repository URL. At home, In Windows, my repository URL is:



<blockquote>file:///E:/svn/projects</blockquote>



and at my _Kubuntu distro_ is:



<blockquote>file://localhost/mnt/sda6/svn</blockquote>



At Linux, you can add those lines to your _/etc/fstab_ file to mount your FAT32 partition every time the system is started:



<blockquote>/dev/sda6 /mnt/sda6 vfat rw,uid=1000,auto  0    0</blockquote>



(/dev/sda6 is my FAT32 partiton and /mnt/sda6 is where my partition's mounting point is)

Just click _Finish_ and try to add your first project to your local repository. If you follow those steps and things don't work, please add comments here.
