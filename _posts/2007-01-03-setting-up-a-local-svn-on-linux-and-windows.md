---
id: 35
title: 'Setting up a local SVN on Linux and Windows'
date: '2007-01-03T23:19:00-02:00'
guid: 'http://rnaufal.wordpress.com/2007/01/03/setting-up-a-local-svn-on-linux-and-windows/'
lj_itemid:
    - '41'
lj_permalink:
    - 'http://rnaufal.livejournal.com/10511.html'
dsq_thread_id:
    - '109779914'
categories:
    - Uncategorized
tags:
    - os_linux
---

I was intended to create a local [SVN](http://subversion.tigris.org/) repository to host my [Eclipse](http://www.eclipse.org/) projects in home. So, I decided to share the same SVN repository on Linux (a *[Kubuntu](http://www.kubuntu.org/) distro*) and Windows, to synchronize my projects in an easy manner. Here are the steps to get the things done:

1. Create a [FAT32](http://en.wikipedia.org/wiki/File_Allocation_Table) partition to host your SVN repository. You cannot configure your local home repository in [NTFS](http://en.wikipedia.org/wiki/NTFS) file system type because Linux can’t write at NTFS partitions.
2. Create a SVN repository on Windows using the [Tortoise](http://tortoisesvn.tigris.org/) utility. This tool is free and makes the repository creation very easy. If you don’t know Tortoise, take a look at the tutorial to be comfortable with the tool. You can create a local repository on any folder in your file system. It’s just click the right button and select *TortoiseSVN -&gt; Create repository here…*
3. So now your repository is created on your local file system. Now you have to download and install Subclipse (if you don’t have downloaded yet :-)), which is an Eclipse plugin to interact with SVN.
4. When you install [Subclipse](http://subclipse.tigris.org/), open your Eclipse platform and go to *Windows -&gt; Preferences -&gt; Team -&gt; SVN* and select *SVNKit (Pure Java)*. This interface allows you to interact with the repository installed on your local machine.
5. Now open the *SVN Repository Exploring perspective*, click the right button and select *New -&gt; Repository Location*. In my machine my SVN repository is configured in other partition (remember this partition has to be FAT32).

The dialog box starts to ask you the SVN repository URL. At home, In Windows, my repository URL is:

> file:///E:/svn/projects

and at my *Kubuntu distro* is:

> file://localhost/mnt/sda6/svn

At Linux, you can add those lines to your */etc/fstab* file to mount your FAT32 partition every time the system is started:

> /dev/sda6 /mnt/sda6 vfat rw,uid=1000,auto 0 0

(/dev/sda6 is my FAT32 partiton and /mnt/sda6 is where my partition’s mounting point is)

Just click *Finish* and try to add your first project to your local repository. If you follow those steps and things don’t work, please add comments here.