---
author: admin
comments: true
date: 2007-04-15 22:53:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2007/04/15/integrating-struts-and-spring/
slug: integrating-struts-and-spring
title: Integrating Struts and Spring
wordpress_id: 38
tags:
- java_programming
---

My coworker Max has argued with me there is no relationship between Java web based frameworks, specially [Struts](http://struts.apache.org/) and [Spring](http://www.springframework.org/). Well, I completelly disagreed with him when he raised this question and here I will post one of the possibilities of their integration. This alternative let you configure Spring to manage your Actions as beans, using the **ContextLoaderPlugin**, and set their dependencies in a Spring context file. Here are the steps to apply this configuration:

Add the following [XML](http://en.wikipedia.org/wiki/XML) snippet to the plug-ins section near the bottom of your **struts-config.xml** file: 



<blockquote><plug-in className="org.springframework.web.struts.ContextLoaderPlugIn"/></blockquote>



Now you can configure your actions to be injected by Spring. One way you can do this is use the **DelegatingActionProxy** class in the type attribute of your **<action-mapping>**. 

This way of configuration allow you to manage your **Actions** and their dependencies in the **action-context.xml** file. The relationship between the Action in **struts-config.xml** and **action-servlet.xml** is established by the action-mapping's
**"path"** and the bean's **"name"**. If you have the following in your **struts-config.xml** file:



<blockquote><action path="/employees" .../></blockquote>



You must define that Action's bean with the **"/users"** name in **action-servlet.xml**:



<blockquote><bean name="/employees" .../></blockquote>



Defining your Action in a context file let you to use Spring's IoC features, as well as instantiate new Actions for each request created. To do this, add **singleton="false"** to your action's bean definition.



<blockquote><bean name="/employees" singleton="false" autowire="byName" class="org.myapplication.web.EmployeeSearchAction"></blockquote>



To be more concrete, here is a complete example of an **Action** described in **struts-config.xml**:



<blockquote><action  input="/index.jsp" name="mainForm" path="/login" scope="request" type="org.springframework.web.struts.DelegatingActionProxy"> <forward name="main_page" path="/main_page.jsp"/> </action></blockquote>



And here is its version in **action-servlet.xml**:



<blockquote><bean id="action.loginAction" singleton="false" autowire="byName" name="/login" class="br.com.rafael.estudoweb.action.LoginAction"/></blockquote>



There are more alternatives to inject your actions in Spring.  If you want to know the other ones, please check out the Spring reference [manual](http://www.springframework.org/documentation).
