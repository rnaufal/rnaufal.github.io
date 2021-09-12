---
author: admin
comments: true
date: 2011-08-25 00:46:52+00:00
layout: post
link: https://rafaelnaufal.com/blog/2011/08/24/some-interesting-maven-tips/
slug: some-interesting-maven-tips
title: Some interesting Maven tips
wordpress_id: 353
tags:
- build
- install
- maven
- modules
- pom
- tips
---

Here are some [Maven](http://maven.apache.org/) tips, extracted from [Javalobby](http://java.dzone.com/articles/5-maven-tips):



	
  * **Maven rf option:** If your project has some modules and the build fails at one of them, it's possible to run the build only at this module, preventing from running the entire build. You can achieve this behavior by executing this command:




<blockquote>mvn -rf my-project clean install</blockquote>



	
  * **Maven pl option:** This option allows you to build specific modules instead of building all projects. You can execute the following command to have this behavior:




<blockquote>mvn -pl my-project-A,my-project-B clean install</blockquote>



This command will build only **my-project-A** and **my-project-B**.


