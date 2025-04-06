---
id: 353
title: 'Some interesting Maven tips'
date: '2011-08-24T21:46:52-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=353'
dsq_thread_id:
    - '395145110'
categories:
    - Uncategorized
tags:
    - build
    - install
    - maven
    - modules
    - pom
    - tips
---

Here are some [Maven](http://maven.apache.org/) tips, extracted from [Javalobby](http://java.dzone.com/articles/5-maven-tips):

- **Maven rf option:** If your project has some modules and the build fails at one of them, it’s possible to run the build only at this module, preventing from running the entire build. You can achieve this behavior by executing this command:
> mvn -rf my-project clean install

- **Maven pl option:** This option allows you to build specific modules instead of building all projects. You can execute the following command to have this behavior:
> mvn -pl my-project-A,my-project-B clean install

This command will build only **my-project-A** and **my-project-B**.