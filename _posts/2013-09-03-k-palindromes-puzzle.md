---
id: 415
title: 'K Palindromes puzzle'
guid: 'http://rafaelnaufal.com/blog/?p=415'
dsq_thread_id:
    - '1701712815'
categories:
    - code
    - languages
    - palindrome
    - programming
    - puzzle
    - ruby
    - string
tags:
    - code
    - languages
    - learning
    - palindrome
    - programming
    - puzzle
    - ruby
    - string
---

Here we have the **K Palindromes** puzzle from [Javalobby](http://java.dzone.com/articles/thursday-code-puzzlerk):

> You probably already know what a palindrome is: a string to results in the same word, whether read left to right, or right to left. A K Palindrome is when a string can be tranformed into a palindrome by changing K characters at most. Regular palindromes have K=0.
> 
> Your challenge today is to write a method which takes a string and a value for k and returns true if it the string qualifies as a K palindrome.

Below is the code in Ruby. Our input string is `omississimo` and it’s a `0 palindrome String`.

```ruby
def isKPalindrome(s, k)
	chars = s.chars.to_a
	limit = chars.size - 1
	count = chars[0...chars.size / 2].each_index.count {|i| !chars[i].eql?(chars[limit - i])}
	k == count ? true : false
end

puts(isKPalindrome("omississimo", 0)) #true
```

The output is `true`. Do you have another solution? Drop your comments here!