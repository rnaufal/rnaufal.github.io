---
id: 398
title: 'Balancing arrays puzzle in Ruby'
guid: 'http://rafaelnaufal.com/blog/?p=398'
dsq_thread_id:
    - '1635008168'
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

> Given an array of numbers, return the index at which the array can be balanced by all numbers on the left side add up the the sum of all numbers of the right side.
> 
> For example, an array with \[1,5,6,7,9,10\] can be balanced by splitting the array at position 4

Here is the solution in Ruby:

```ruby
v=[1,5,6,7,9,10];sum = v.reduce(:+);count=0;index = (0...v.size).detect { |i| count += v[i]; count * 2 == sum};index == nil ? nil : index + 1
```

The input array `[1,5,6,7,9,10]` will split the array at position **4**, as stated above.

Any other solutions? Drop comments here 🙂