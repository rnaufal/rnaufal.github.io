---
author: admin
comments: true
date: 2013-08-12 02:11:07+00:00
layout: post
link: https://rafaelnaufal.com/blog/2013/08/11/finding-the-second-highest-frequency/
slug: finding-the-second-highest-frequency
title: Finding the second highest frequency
wordpress_id: 386
categories:
- code
- languages
- programming
- puzzle
- ruby
tags:
- code
- languages
- learning
- programming
- puzzle
- ruby
---

It's been a long time since I posted for the last time, but I promise I'll try to keep this blog up-to-date :-)

One of the purposes of this blog is to explore new technologies and recently I've been studying [Ruby](http://www.ruby-lang.org/) solving some puzzles posted by [](http://java.dzone.com/users/jsugrue) on [JavaLobby](http://java.dzone.com/).

The problem is about finding the [second highest frequency](http://java.dzone.com/articles/thursday-code-puzzler-second) of a character in a String. Below is the Ruby code, using the powerful concept of Ruby [closures](http://en.wikipedia.org/wiki/Closure_%28computer_science%29).


    
    v="aabbbc".chars;h=Hash[v.map{|k| [k, v.count(k)] }];max=h.values.max;found=h.select { |k, v| v < max};found.keys.first if found



For the input String `"aabbbc"`, the result is `"a"`. I could done it in a more [OOP](http://en.wikipedia.org/wiki/Object-oriented_programming) style, but I chose a more concise solution :-)

If you have another version in Ruby, feel free to post a comment!
