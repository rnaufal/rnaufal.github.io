---
id: 73
title: 'Using Scala to update LiveJournal tags &#8211; Part I'
date: '2009-05-23T13:45:00-03:00'
guid: 'http://rnaufal.wordpress.com/2009/05/23/using-scala-to-update-livejournal-tags-part-i/'
lj_itemid:
    - '82'
lj_permalink:
    - 'http://rnaufal.livejournal.com/21132.html'
dsq_thread_id:
    - '102873622'
categories:
    - Uncategorized
tags:
    - closures
    - functional
    - java
    - jvm
    - programming
    - scala
---

Some days ago I started to use the [Scala](http://www.scala-lang.org/) programming language to update my Livejournal tags using its [XML-RPC](http://en.wikipedia.org/wiki/XML-RPC) protocol reference. First I had to check if some tags of mine were entered wrong, so I’ve done this Scala program to list all of them:

```
<span class="syntax0"><span class="gutter">   1:</span><span class="syntax8">import</span> org.apache.xmlrpc.client.XmlRpcClient;
<span class="gutter">   2:</span><span class="syntax8">import</span> org.apache.xmlrpc.client.XmlRpcClientConfigImpl;
<span class="gutter">   3:</span><span class="syntax8">import</span> org.apache.xmlrpc.client.XmlRpcCommonsTransportFactory;
<span class="gutter">   4:</span><span class="syntax8">import</span> java.net.URL;
<span class="gutterH">   5:</span><span class="syntax8">import</span> java.util.Map
<span class="gutter">   6:</span><span class="syntax8">import</span> java.util.HashMap
<span class="gutter">   7:</span><span class="syntax8">import</span> scala.collection.immutable.TreeSet
<span class="gutter">   8:</span>
<span class="gutter">   9:</span><span class="syntax8">object</span> LJListTag <span class="syntax18">{</span>
<span class="gutterH">  10:</span>     <span class="syntax8">def</span> <span class="syntax6">main</span>(args: <span class="syntax10">Array</span><span class="syntax15">[String]</span>) <span class="syntax18">{</span>
<span class="gutter">  11:</span>         <span class="syntax8">val</span> config <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax6">XmlRpcClientConfigImpl</span>()
<span class="gutter">  12:</span>         config.<span class="syntax6">setEnabledForExtensions</span>(<span class="syntax8">true</span>);
<span class="gutter">  13:</span>         config.<span class="syntax6">setServerURL</span>(<span class="syntax8">new</span> <span class="syntax6">URL</span>(<span class="syntax13">"</span><span class="syntax13">http://www.livejournal.com/interface/xmlrpc</span><span class="syntax13">"</span>))
<span class="gutter">  14:</span>         <span class="syntax8">val</span> client <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax6">XmlRpcClient</span>()
<span class="gutterH">  15:</span>         client.<span class="syntax6">setConfig</span>(config)
<span class="gutter">  16:</span>         <span class="syntax8">val</span> params <span class="syntax18">=</span> <span class="syntax8">new</span> HashMap<span class="syntax15">[String,</span><span class="syntax15"> </span><span class="syntax15">String]</span>
<span class="gutter">  17:</span>         params.<span class="syntax6">put</span>(<span class="syntax13">"</span><span class="syntax13">username</span><span class="syntax13">"</span>, <span class="syntax13">"</span><span class="syntax13">user</span><span class="syntax13">"</span>)
<span class="gutter">  18:</span>         params.<span class="syntax6">put</span>(<span class="syntax13">"</span><span class="syntax13">password</span><span class="syntax13">"</span>, <span class="syntax13">"</span><span class="syntax13">password</span><span class="syntax13">"</span>)
<span class="gutter">  19:</span>         <span class="syntax8">var</span> paramsToServer <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax10">Array</span><span class="syntax15">[Object]</span>(<span class="syntax5">1</span>)
<span class="gutterH">  20:</span>         <span class="syntax6">paramsToServer</span>(<span class="syntax5">0</span>) <span class="syntax18">=</span> params
<span class="gutter">  21:</span>         <span class="syntax8">val</span> results <span class="syntax18">=</span> client.<span class="syntax6">execute</span>(<span class="syntax13">"</span><span class="syntax13">LJ.XMLRPC.getusertags</span><span class="syntax13">"</span>, paramsToServer).asInstanceOf<span class="syntax15">[Map[String,</span><span class="syntax15"> </span><span class="syntax15">String]]</span>;
<span class="gutter">  22:</span>         <span class="syntax6">printEachTag</span>(results)
<span class="gutter">  23:</span>     <span class="syntax18">}</span>
<span class="gutter">  24:</span>    
<span class="gutterH">  25:</span>     <span class="syntax8">def</span> <span class="syntax6">printEachTag</span>(results: Map<span class="syntax15">[String,</span><span class="syntax15"> </span><span class="syntax15">String]</span>) <span class="syntax18">{</span>
<span class="gutter">  26:</span>        <span class="syntax8">var</span> allTags <span class="syntax18">=</span> <span class="syntax8">new</span> TreeSet<span class="syntax15">[String]</span>
<span class="gutter">  27:</span>        <span class="syntax8">val</span> iterator <span class="syntax18">=</span> results.<span class="syntax6">values</span>().<span class="syntax6">iterator</span>()
<span class="gutter">  28:</span>           <span class="syntax8">while</span>(iterator.<span class="syntax6">hasNext</span>()) <span class="syntax18">{</span>
<span class="gutter">  29:</span>             <span class="syntax8">val</span> resultFromRPCData <span class="syntax18">=</span> iterator.<span class="syntax6">next</span>().asInstanceOf<span class="syntax15">[Array[Any]]</span>
<span class="gutterH">  30:</span>             resultFromRPCData.<span class="syntax6">foreach</span>(singleResult <span class="syntax18">=</span><span class="syntax18">></span> allTags <span class="syntax18">+</span><span class="syntax18">=</span> <span class="syntax6">extractTag</span>(singleResult))
<span class="gutter">  31:</span>           <span class="syntax18">}</span>
<span class="gutter">  32:</span>        allTags.<span class="syntax6">foreach</span>(tag <span class="syntax18">=</span><span class="syntax18">></span> <span class="syntax6">println</span>(tag))
<span class="gutter">  33:</span>     <span class="syntax18">}</span>
<span class="gutter">  34:</span>    
<span class="gutterH">  35:</span>    <span class="syntax8">def</span> <span class="syntax6">extractTag</span>(singleResult: <span class="syntax10">Any</span>): <span class="syntax10">String</span> <span class="syntax18">=</span> <span class="syntax18">{</span>
<span class="gutter">  36:</span>        <span class="syntax8">val</span> tag <span class="syntax18">=</span> singleResult.asInstanceOf<span class="syntax15">[HashMap[String,</span><span class="syntax15"> </span><span class="syntax15">String]]</span>
<span class="gutter">  37:</span>        <span class="syntax8">return</span> tag.<span class="syntax6">get</span>(<span class="syntax13">"</span><span class="syntax13">name</span><span class="syntax13">"</span>)
<span class="gutter">  38:</span>    <span class="syntax18">}</span>
<span class="gutter">  39:</span><span class="syntax18">}</span>
</span>
```

Just fill your user and password to have all of your LiveJournal tags printed on the standard output. The experience was so amazing, since you can use all the Java libraries (Scala is fully interoperable with Java and runs on top of the JVM). I used a [TreeSet](http://www.scala-lang.org/docu/files/api/scala/collection/immutable/TreeSet$object.html) because I wanted print my tags sorted according its alphabetical order. I’m continuously studying Scala and its API, so the code above doesn’t use any advanced Scala constructs. If you have any suggestion about the code or how to use better the Scala constructs, post your comments here. It will be all appreciated.