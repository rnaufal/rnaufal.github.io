---
author: admin
comments: true
date: 2013-08-28 21:02:34+00:00
layout: post
link: https://rafaelnaufal.com/blog/2013/08/28/minimum-difference-puzzle-in-ruby/
slug: minimum-difference-puzzle-in-ruby
title: Minimum difference puzzle in Ruby
wordpress_id: 410
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

Folks, here we are for another puzzle from [Javalobby](http://java.dzone.com/articles/thursday-code-puzzler-minimum): 



<blockquote>Given two arrays, sorted and exactly the same length, write a function that finds a pair of numbers - one from each of the arrays - such that the difference between both is as small as possible.</blockquote>



Suppose our input arrays are `[1,2,3,4,5]` and `[6,7,8,9,10]`. Below is my solution in Ruby, it's a one liner code :-):


    
    [1,2,3,4,5].product([6,7,8,9,10]).map {|x, y| [x, y, (x-y).abs]}.sort { |a, b| a.last<=> b.last }.first.take(2)



The output is `[5, 6]`.

Have another solution? Leave your comments here!
