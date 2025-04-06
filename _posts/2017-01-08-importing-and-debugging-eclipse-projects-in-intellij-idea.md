---
id: 515
title: 'Importing and debugging Eclipse projects in IntelliJ IDEA'
date: '2017-01-08T20:03:45-02:00'
guid: 'http://rafaelnaufal.com/blog/?p=515'
dsq_thread_id:
    - '5446739941'
categories:
    - debug
    - eclipse
    - idea
    - intellij
    - java
tags:
    - debug
    - eclipse
    - idea
    - intellij
    - java
---

Last week I faced a situation to import some [Eclipse](https://eclipse.org/) projects to [IntelliJ IDEA](https://www.jetbrains.com/idea/), my default Java IDE. IntelliJ IDEA supports this integration, just go to `File > New > Project from Existing Sources…` and select a directory where Eclipse *.project* or *.classpath* files are located.

The project was imported successfully, it had some test compilation errors and it was all done for that moment. But, after running the project, I noted that I couldn’t debug some classes as well as I got used at Eclipse.

It was because, by default, IntelliJ IDEA uses the [javac](https://en.wikipedia.org/wiki/Javac) compiler and Eclipse has its own Java compiler that is part of [JDT](https://eclipse.org/jdt/core/) core. IntelliJ IDEA doesn’t proceed on code compilation when it finds the first error, even for test code or code that isn’t part of the build. The Eclipse compiler is able to proceed on code compilation even if it has compilation errors, so it is possible to run / debug code that doesn’t compile at all.

The solution, in this case, is to switch IntelliJ IDEA to use the Eclipse compiler. Just go to `File > Settings > Build, Execution, Deployment > Compiler > Java compiler` and change the drop down box `"Use compiler:"` to `Eclipse` and that is done.

I did that and now I am able to run / debug the Eclipse project using IntelliJ IDEA very well.

I have found the solution here:

[Enable Partial Compile IntelliJ](http://stackoverflow.com/a/16784855)  
[What is the difference between javac and the Eclipse compiler?](http://stackoverflow.com/a/3061680)

Have you faced a situation like this? Have you done another solution than mine? Drop your comments here! 🙂