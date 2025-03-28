---
id: 72
title: '&#8220;Salute #{@Ruby}!&#8221;'
date: '2009-05-21T22:15:00-03:00'
author: rnaufal
layout: single
guid: 'http://rnaufal.wordpress.com/2009/05/21/salute-ruby/'
lj_itemid:
    - '81'
lj_permalink:
    - 'http://rnaufal.livejournal.com/20964.html'
dsq_thread_id:
    - '102750193'
categories:
    - Uncategorized
tags:
    - blocks
    - closures
    - parser
    - programming
    - ruby
    - xml
---

Some times ago I had to parse a XML messages’ file to produce some [i18n](http://en.wikipedia.org/wiki/Internationalization_and_localization) properties files.

I decided to try it with Ruby, mainly because of two reasons:

1. I’m continuosly exploring some dynamically-typed languages, like Python and Ruby
2. I wanted to try the *conciseness* of programming with closures

So, I used the [REXML](http://www.germane-software.com/software/rexml/) API to process the XML file. The result code looks like the one below:

```
<span class="syntax0"><span class="gutter">   1:</span><span class="syntax9">require</span> <span class="syntax13">'</span><span class="syntax13">rexml/document</span><span class="syntax13">'</span>
<span class="gutter">   2:</span><span class="syntax9">include</span> REXML
<span class="gutter">   3:</span>englishFile <span class="syntax18">=</span> File.new<span class="syntax18">(</span><span class="syntax13">'</span><span class="syntax13">englishFileName</span><span class="syntax13">'</span>, <span class="syntax13">'</span><span class="syntax13">w+</span><span class="syntax13">'</span><span class="syntax18">)</span>
<span class="gutter">   4:</span>spanishFile <span class="syntax18">=</span> File.new<span class="syntax18">(</span><span class="syntax13">'</span><span class="syntax13">spanishFileName</span><span class="syntax13">'</span>, <span class="syntax13">'</span><span class="syntax13">w+</span><span class="syntax13">'</span><span class="syntax18">)</span>
<span class="gutterH">   5:</span>portugueseFile <span class="syntax18">=</span> File.new<span class="syntax18">(</span><span class="syntax13">'</span><span class="syntax13">portugueseFileName</span><span class="syntax13">'</span>, <span class="syntax13">'</span><span class="syntax13">w+</span><span class="syntax13">'</span><span class="syntax18">)</span>
<span class="gutter">   6:</span>errorMessagesFile <span class="syntax18">=</span> File.new<span class="syntax18">(</span><span class="syntax13">"</span><span class="syntax13">errorMessages</span><span class="syntax13">.</span><span class="syntax13">xml</span><span class="syntax13">"</span><span class="syntax18">)</span>
<span class="gutter">   7:</span>document <span class="syntax18">=</span> Document.new<span class="syntax18">(</span>file<span class="syntax18">)</span>
<span class="gutter">   8:</span>root <span class="syntax18">=</span> document.root
<span class="gutter">   9:</span>root.each_element<span class="syntax18">(</span><span class="syntax13">"</span><span class="syntax13">Property</span><span class="syntax13">"</span><span class="syntax18">)</span> <span class="syntax8">do</span> <span class="syntax18">|</span>propertyTag<span class="syntax18">|</span>
<span class="gutterH">  10:</span>  id <span class="syntax18">=</span> propertyTag.attributes<span class="syntax18">[</span><span class="syntax13">'</span><span class="syntax13">id</span><span class="syntax13">'</span><span class="syntax18">]</span>   
<span class="gutter">  11:</span>  propertyTag.each_element<span class="syntax18">(</span><span class="syntax13">"</span><span class="syntax13">element</span><span class="syntax13">"</span><span class="syntax18">)</span> <span class="syntax8">do</span> <span class="syntax18">|</span>elementTag<span class="syntax18">|</span>
<span class="gutter">  12:</span>      elementAttr <span class="syntax18">=</span> elementTag.attributes<span class="syntax18">[</span><span class="syntax13">'</span><span class="syntax13">otherTag</span><span class="syntax13">'</span><span class="syntax18">]</span>
<span class="gutter">  13:</span>      error <span class="syntax18">=</span> elementTag.text <span class="syntax18">=</span><span class="syntax18">=</span> <span class="syntax10">nil</span> <span class="syntax18">?</span> <span class="syntax13">"</span><span class="syntax13">"</span> <span class="syntax18">:</span> <span class="syntax13">"</span><span class="syntax18">#{</span>id<span class="syntax18">}</span><span class="syntax13"> </span><span class="syntax13">=</span><span class="syntax13"> </span><span class="syntax18">#{</span>elementTag.text<span class="syntax18">}</span><span class="syntax13">\n</span><span class="syntax13">"</span>
<span class="gutter">  14:</span>      <span class="syntax8">if</span> elementAttr <span class="syntax18">=</span> <span class="syntax13">"</span><span class="syntax13">pt</span><span class="syntax13">"</span>
<span class="gutterH">  15:</span>          portugueseFile <span class="syntax18"><<</span> error
<span class="gutter">  16:</span>      <span class="syntax8">elsif</span> elementAttr <span class="syntax18">=</span><span class="syntax18">=</span> <span class="syntax13">"</span><span class="syntax13">es</span><span class="syntax13">"</span>
<span class="gutter">  17:</span>          spanishFile <span class="syntax18"><<</span> error
<span class="gutter">  18:</span>      <span class="syntax8">else</span> 
<span class="gutter">  19:</span>          portugueseFile <span class="syntax18"><<</span> error
<span class="gutterH">  20:</span>      <span class="syntax8">end</span>
<span class="gutter">  21:</span>  <span class="syntax8">end</span>
<span class="gutter">  22:</span><span class="syntax8">end</span>
<span class="gutter">  23:</span>errorMessagesFile.close<span class="syntax18">(</span><span class="syntax18">)</span>
<span class="gutter">  24:</span>englishFile.close<span class="syntax18">(</span><span class="syntax18">)</span>
<span class="gutterH">  25:</span>spanishFile.close<span class="syntax18">(</span><span class="syntax18">)</span>
<span class="gutter">  26:</span>portugueseFile.close<span class="syntax18">(</span><span class="syntax18">)</span>
<span class="gutter">  27:</span>  
</span>
```

I like to solve this kind of tasks with programming languages (mainly the dynamically-typed ones..) I don’t know very much because it’s an opportunity to put my hands on them! This way I could experience Ruby’s *closures* syntax, it was really nice and I’m gonna try something new with it often!

*\*Updated: line 13*