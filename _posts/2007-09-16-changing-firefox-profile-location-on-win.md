---
id: 49
title: 'Changing Firefox profile location on Win'
date: '2007-09-16T23:04:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2007/09/16/changing-firefox-profile-location-on-win/'
lj_itemid:
    - '55'
lj_permalink:
    - 'http://rnaufal.livejournal.com/14214.html'
dsq_thread_id:
    - '102750791'
categories:
    - Uncategorized
tags:
    - firefox
    - tech
---

Some days ago I finally had enough time to move all my *Documents and Settings* folder to a dedicated partition, storing my *Home* directory and files (I already know it’s very late for this…don’t have to remember me..). So, I was looking for a way to change the [Firefox](http://www.mozilla.com/en-US/firefox/) default profile location to this partition, keeping it safely separated from the installation files. It’s quite easy, the steps are as follws:

- In Windows 2000 and XP, you should find your profile in: C:\\Documents and Settings\\{user name}\\Application Data\\Mozilla\\Firefox\\Profiles. The Application Data folder is by default a hidden folder in Windows, so if you do not see an Application Data folder, check the Folder Options and make sure the option “Show hidden files and folders” is checked.
- Open the *profiles.ini* file, on the *Profiles* folder. Open it. Do not use Word or a word processor because these programs typically save weird characters when they save a file. You need to use a pure text editor like [Notepad++](http://notepad-plus.sourceforge.net/).
- You have to make two changes to the *profiles.ini* file. First, change **IsRelative=1** to **IsRelative=0**. This changes the path from relative to absolute. Second, fully specify the new path to the new location of the Profiles folder and the default file folder. The new contents of the file seems like this one:  
    > \[General\]  
    > StartWithLastProfile=1
    > 
    > \[Profile0\]  
    > Name=default  
    > IsRelative=0  
    > Path=E:\\Rafael\\firefox\_profile\\profile.default
- If you have any extensions, you have to open the *extensions.ini* file on your new profile directory (in this case, E:\\Rafael\\firefox\_profile\\profile.default) and replace any reference to the older directory to the new one. My new *extensions.ini* file looks like this:  
    > \[ExtensionDirs\]  
    > Extension0=E:\\Rafael\\firefox\_profile\\profile.default\\extensions\\{34274bf4-1d97-a289-e984-17e546307e4f}  
    > Extension1=E:\\Rafael\\firefox\_profile\\profile.default\\extensions\\{6AC85730-7D0F-4de0-B3FA-21142DD85326}  
    > .  
    > .  
    > .  
    > \[ThemeDirs\]  
    > Extension0=C:\\Program Files\\Mozilla Firefox\\extensions\\{972ce4c6-7e08-4474-a285-3208198ce6fd}  
    > Extension1=E:\\Rafael\\firefox\_profile\\profile.default\\extensions\\{eb46c787-131a-4eb7-9b93-7f62ca550917}

So I think this should works. Save those files and restart Firefox. Soon I will make these changes on my Linux [kubuntu](http://www.kubuntu.org/) distro!