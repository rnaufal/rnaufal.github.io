---
id: 410
title: 'Minimum difference puzzle in Ruby'
date: '2013-08-28T18:02:34-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=410'
dsq_thread_id:
    - '1661474600'
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

> Given two arrays, sorted and exactly the same length, write a function that finds a pair of numbers – one from each of the arrays – such that the difference between both is as small as possible.

Suppose our input arrays are `[1,2,3,4,5]` and `[6,7,8,9,10]`. Below is my solution in Ruby, it’s a one liner code :-):

```
[1,2,3,4,5].product([6,7,8,9,10]).map {|x, y| [x, y, (x-y).abs]}.sort { |a, b| a.last<=> b.last }.first.take(2)
```

The output is `[5, 6]`.

Have another solution? Leave your comments here!