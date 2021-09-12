---
author: admin
comments: true
date: 2013-08-23 20:37:21+00:00
layout: post
link: https://rafaelnaufal.com/blog/2013/08/23/balancing-arrays-puzzle-in-ruby/
slug: balancing-arrays-puzzle-in-ruby
title: Balancing arrays puzzle in Ruby
wordpress_id: 398
categories:
- arrays
- code
- languages
- programming
- puzzle
- ruby
tags:
- array
- arrays
- code
- languages
- learning
- programming
- puzzle
- ruby
---

Here we are for another puzzle from [Javalobby](http://java.dzone.com/articles/thursday-code-puzzler-12): 



<blockquote>Given an array of numbers,  return the index at which the array can be balanced by all numbers on the left side add up the the sum of all numbers of the right side.

For example, an array with [1,5,6,7,9,10] can be balanced by splitting the array at position 4</blockquote>



Here is the solution in Ruby:


    
    v=[1,5,6,7,9,10];sum = v.reduce(:+);count=0;index = (0...v.size).detect { |i| count += v[i]; count * 2 == sum};index == nil ? nil : index + 1



The input array `[1,5,6,7,9,10]` will split the array at position **4**, as stated above.

Any other solutions? Drop comments here :-)
