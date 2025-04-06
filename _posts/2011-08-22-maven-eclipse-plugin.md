---
id: 338
title: 'Maven Eclipse plugin using project dependencies'
date: '2011-08-22T23:09:43-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=338'
dsq_thread_id:
    - '393877427'
categories:
    - Uncategorized
tags:
    - classpath
    - eclipse
    - goal
    - maven
    - plugin
    - project
---

Some months ago I was noting the behavior of the Maven Eclipse plugin during the `eclipse:eclipse` goal.

I realized that its default behavior is to build the dependencies based on the Eclipse projects instead of the installed packages on the repository. During development time, it’s the behavior we need, but if you want to build the Eclipse files using the packages on the repository, you have to use the following command:

> mvn eclipse:eclipse -Declipse.useProjectReferences=false

By default, the `useProjectReferences` flag is set to `true`, in other words, the plugin will create and reference the projects in Eclipse. Without it you’ll have to use `mvn install` to make changes available for dependent projects. Very interesting to note.

**Update \*:** *After creating the project dependencies, you have to execute `mvn install` to make it available for `mvn eclipse:eclipse` on dependent projects for the first time.*