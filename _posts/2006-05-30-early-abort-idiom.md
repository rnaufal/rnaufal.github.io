---
id: 8
title: 'Early abort idiom'
date: '2006-05-30T16:07:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2006/05/30/early-abort-idiom/'
lj_itemid:
    - '3'
lj_permalink:
    - 'http://rnaufal.livejournal.com/774.html'
dsq_thread_id:
    - '102872830'
categories:
    - Uncategorized
tags:
    - software
---

Take a look at those [Java](http://java.sun.com) code snippets:

``

> public void insert(Order order)  
>  if(order != null) {  
>  // insert code here  
>  }  
> }  
>   
> public void insert(Order order)  
>  if(order == null) {  
>  return;  
>  }  
>  // insert code here  
> }

The second code scratch is said to increase the Thomas McCabe’s [cyclomatic complexity](http://en.wikipedia.org/wiki/Cyclomatic_complexity). The cyclomatic complexity is a model metric instead of implementation metric, as you may think. An example about implementation metric is [LOC ](http://en.wikipedia.org/wiki/Source_lines_of_code)(Lines of Code). When I was in college, I learned the McCabe’s metric measures the number of control flow statements and return statements of your code, but it doesn’nt count the normal return statement of your methods. So, the McCabe metric is two for the first code and two for the second. McCabe says that the computation complexity rises with the increase of the execution routes. [Cedric](http://www.beust.com/weblog/archives/000308.html) has an interesting opinion about this subject. Particularly, I think when you try to use the first *insert(Order order)*, you end up having some nested *if’s*, your code tends to be a little messy. The second one focus on the basic flow of your method, that is, the normal bahavior its expected to have. In my daily basis, sometimes I apply the first one, sometimes the second one. And you? Do you think in cyclomatic complexity when you are coding?