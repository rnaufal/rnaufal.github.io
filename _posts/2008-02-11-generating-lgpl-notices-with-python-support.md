---
id: 61
title: 'Generating LGPL notices with Python support'
date: '2008-02-11T00:19:00-02:00'
guid: 'http://rnaufal.wordpress.com/2008/02/11/generating-lgpl-notices-with-python-support/'
lj_itemid:
    - '69'
lj_permalink:
    - 'http://rnaufal.livejournal.com/17681.html'
dsq_thread_id:
    - '102742847'
categories:
    - Uncategorized
tags:
    - java_programming
    - jfilecontentmanager
    - lgpl
    - ooad
    - python
---

When we started developing [JFileContentManager](http://rnaufal.livejournal.com/16871.html), we didn’t even think to release it as an open-source project. So, when we finished the project, I particularly thought about this idea, because I was very interested in participating on an community involving project. So, we decided to release it under the [LGPL](http://www.gnu.org/licenses/lgpl.html) licence, because we wanted the project audience to be wider as possible. But, before turning it public, we needed to add the LGPL license term to every [Java](http://java.sun.com/) file of the project.  
Opening and editing each Java class, one by one, would be a tedious task, taking a lot of time and adding up to the fact I’m very interested on learning dynamic languages (like [Python](http://www.python.org/), [Ruby](http://www.ruby-lang.org/)), I developed a Python script to automate this task for us. Our Python code is intended to open each Java file, adding the license term on the start of the file as a Java comment and writing it to the disk. The script is as follows:

```python
# Python script to add the LGPL notices to each java file of the FileContentManager project.
import os, glob, sys
License = """\
/**
*FileContentManager is a Java based file manager desktop application,
*it can show, edit and manipulate the content of the files archived inside a zip.
*
*Copyright (C) 2008
*
*Created by Camila Sanchez [http://mimix.wordpress.com/], Rafael Naufal [http://rnaufal.livejournal.com]
and Rodrigo [rdomartins@gmail.com]
*
*FileContentManager is free software; you can redistribute it and/or
*modify it under the terms of the GNU Lesser General Public
*License as published by the Free Software Foundation; either
*version 2.1 of the License, or (at your option) any later version.
*
*This library is distributed in the hope that it will be useful,
*but WITHOUT ANY WARRANTY; without even the implied warranty of
*MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
*Lesser General Public License for more details.
*
*You should have received a copy of the GNU Lesser General Public
*License along with FileContentManager; if not, write to the Free Software
*Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA """
        
size = len(sys.argv)
if size == 1 or size > 
            print "Usage: AddLicense.py $1"
            sys.exit(1)
inputPath = sys.argv[1]
        if not os.path.exists(inputPath):
            print inputPath, "does not exist on disk"
            sys.exit(1)
if not os.path.isdir(inputPath):
            print inputPath, "isn't a dir"
            sys.exit(1)
for path, dirs, files in os.walk(inputPath):
            fileWithLicense = ''
            for filepath in [ os.path.join(path, f)
            for f in files if f.endswith(".java")]:
                content = file(filepath).read()
        f = file(filepath, "w")
        print >>f, License + "\n" + content
        f.close()
```

`License` is a Python multiline string, denoted by the triple-quotes. The main action begins with the `os.walk()` expression that walks every file in the directory, entered by the user as a comannd line argument, like this:

```python
python AddLicense.py ${path}
```

 where `${path}` defines user project root directory. The list comprehension syntax produces the full path of each of the Java files. When the match is found, the file is opened and its content is assigned to the variable `content`. So, the License string is added to the start of the file and the file is then written to the disk. The print statements use a redirection syntax, for example: `print >>f, License + "\n" + content`. The ‘&gt;&gt;f’ sends the results to `f` rather than the console. So, this Python script helped our team to release the project early and at the same time automated the task of adding the LGPL notices. I think Python is very useful for these kind of tasks. And you?