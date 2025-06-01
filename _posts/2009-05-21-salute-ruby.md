---
id: 72
title: '&#8220;Salute #{@Ruby}!&#8221;'
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

```ruby
require 'rexml/document'
include REXML
englishFile = File.new('englishFileName', 'w+')
spanishFile = File.new('spanishFileName', 'w+')
portugueseFile = File.new('portugueseFileName', 'w+')
errorMessagesFile = File.new("errorMessages.xml")
document = Document.new(file)
root = document.root
root.each_element("Property") do |propertyTag|
  id = propertyTag.attributes['id']   
  propertyTag.each_element("element") do |elementTag|
      elementAttr = elementTag.attributes['otherTag']
      error = elementTag.text == nil ? "" : "#{id} = #{elementTag.text}\n"
      if elementAttr = "pt"
          portugueseFile << error
      elsif elementAttr == "es"
          spanishFile << error
      else 
          portugueseFile << error
      end
  end
end
errorMessagesFile.close()
englishFile.close()
spanishFile.close()
portugueseFile.close()
```

I like to solve this kind of tasks with programming languages (mainly the dynamically-typed ones..) I don’t know very much because it’s an opportunity to put my hands on them! This way I could experience Ruby’s *closures* syntax, it was really nice and I’m gonna try something new with it often!

*\*Updated: line 13*