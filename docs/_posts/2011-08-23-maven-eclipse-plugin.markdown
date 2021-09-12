---
author: admin
comments: true
date: 2011-08-23 02:09:43+00:00
layout: post
link: https://rafaelnaufal.com/blog/2011/08/22/maven-eclipse-plugin/
slug: maven-eclipse-plugin
title: Maven Eclipse plugin using project dependencies
wordpress_id: 338
tags:
- classpath
- eclipse
- goal
- maven
- plugin
- project
---

Some months ago I was noting the behavior of the Maven Eclipse plugin during the `eclipse:eclipse` goal.

I realized that its default behavior is to build the dependencies based on the Eclipse projects instead of the installed packages on the repository. During development time, it's the behavior we need, but if you want to build the Eclipse files using the packages on the repository, you have to use the following command:



<blockquote>mvn eclipse:eclipse -Declipse.useProjectReferences=false</blockquote>



By default, the `useProjectReferences` flag is set to `true`, in other words, the plugin will create and reference the projects in Eclipse. Without it you'll have to use `mvn install` to make changes available for dependent projects. Very interesting to note.

**Update *: **_After creating the project dependencies, you have to execute `mvn install` to make it available for `mvn eclipse:eclipse` on dependent projects for the first time._
