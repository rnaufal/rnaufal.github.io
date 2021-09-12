---
author: admin
comments: true
date: 2007-11-20 02:16:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2007/11/19/swing-tips-and-tricks/
slug: swing-tips-and-tricks
title: Swing tips and tricks
wordpress_id: 54
tags:
- java
- programming
- swing
---

Some days go I was given the task to customize the Java Swing widgets for a project in our company.  The default look and feel of a [JDialog](http://java.sun.com/javase/6/docs/api/javax/swing/JDialog.html), specifically, has the [Java](http://java.sun.com) logo trademark icon on the upper corner left, the close button on the right one and the title panel is painted according to the default [MetalLookAndFeel](http://java.sun.com/j2se/1.5.0/docs/api/javax/swing/plaf/metal/MetalLookAndFeel.html) probably. As an example, we have something like this:



![](http://br.geocities.com/rsilvasp/dialog.JPG)



We wanna have an option to change the title's panel color, to remove the close button and not to have the Java trademark logo showing on the panel. The final JDialog should look like this:



![](http://br.geocities.com/rsilvasp/dialog_new.JPG)



I've thought it was a nearly difficult task, because I had to override a default look and feel and some hidden properties, sometimes difficult to find. Shame on me. Searching through some forums, I've found some interesting tips and tricks about how to customize a the entire dialogs of a Swing application, even without creating a look and feel or overriding an old one. 

For your knowledge, here are some overridden properties to make the JDialog seems like the latter above. These properties let you define new colors for the active caption of your widgets, other font colors, custom family types and much more (for other properties see through the documentation API or the forums below).



<blockquote>UIManager.put("activeCaption", Color.BLUE);
UIManager.put("activeCaptionText", Color.WHITE);
UIManager.put("InternalFrame.titleFont", new Font("Arial-12-i-2", Font.BOLD, 11));
Border cuverdBorder = new LineBorder(new Color(210, 210, 210), 2, true);
dialog.getRootPane().setBorder(cuverdBorder);
dialog.getRootPane().setWindowDecorationStyle(JRootPane.PLAIN_DIALOG);
JDialog.setDefaultLookAndFeelDecorated(true);
JFrame.setDefaultLookAndFeelDecorated(true);
dialog.setUndecorated(true);		
</blockquote>



As a little example, below is the Java code to remove the close button from the panel's title. This little code snippet below traverses the component hierarchy, passed as a parameter, in a recursive method.


    
    <span class="gutter">   1:</span><span class="syntax8">public</span> <span class="syntax8">static</span> <span class="syntax10">void</span> <span class="syntax6">removeCloseButton</span><span class="syntax18">(</span>Component comp<span class="syntax18">)</span>
    <span class="gutter">   2:</span><span class="syntax18">{</span>
    <span class="gutter">   3:</span>    <span class="syntax8">if</span> <span class="syntax18">(</span>comp <span class="syntax8">instanceof</span> AbstractButton<span class="syntax18">)</span>
    <span class="gutter">   4:</span>    <span class="syntax18">{</span>
    <span class="gutterH">   5:</span>        Action action <span class="syntax18">=</span> <span class="syntax18">(</span><span class="syntax18">(</span>AbstractButton<span class="syntax18">)</span> comp<span class="syntax18">)</span>.<span class="syntax6">getAction</span><span class="syntax18">(</span><span class="syntax18">)</span>;
    <span class="gutter">   6:</span>        String cmd <span class="syntax18">=</span> <span class="syntax18">(</span>action <span class="syntax18">=</span><span class="syntax18">=</span> <span class="syntax14">null</span><span class="syntax18">)</span> ? <span class="syntax13">"</span><span class="syntax13">"</span> : action.<span class="syntax6">toString</span><span class="syntax18">(</span><span class="syntax18">)</span>;
    <span class="gutter">   7:</span>        <span class="syntax8">if</span> <span class="syntax18">(</span>cmd.<span class="syntax6">contains</span><span class="syntax18">(</span><span class="syntax13">"</span><span class="syntax13">CloseAction</span><span class="syntax13">"</span><span class="syntax18">)</span><span class="syntax18">)</span>
    <span class="gutter">   8:</span>        <span class="syntax18">{</span>
    <span class="gutter">   9:</span>            comp.<span class="syntax6">getParent</span><span class="syntax18">(</span><span class="syntax18">)</span>.<span class="syntax6">remove</span><span class="syntax18">(</span>comp<span class="syntax18">)</span>;
    <span class="gutterH">  10:</span>        <span class="syntax18">}</span>
    <span class="gutter">  11:</span>    <span class="syntax18">}</span> <span class="syntax8">else</span> <span class="syntax8">if</span> <span class="syntax18">(</span>comp <span class="syntax8">instanceof</span> Container<span class="syntax18">)</span>
    <span class="gutter">  12:</span>    <span class="syntax18">{</span>
    <span class="gutter">  13:</span>        Component[] children <span class="syntax18">=</span> <span class="syntax18">(</span><span class="syntax18">(</span>Container<span class="syntax18">)</span> comp<span class="syntax18">)</span>.<span class="syntax6">getComponents</span><span class="syntax18">(</span><span class="syntax18">)</span>;
    <span class="gutter">  14:</span>        <span class="syntax8">for</span> <span class="syntax18">(</span><span class="syntax10">int</span> i <span class="syntax18">=</span> <span class="syntax5">0</span>; i <span class="syntax18"><</span> children.length; <span class="syntax18">+</span><span class="syntax18">+</span>i<span class="syntax18">)</span>
    <span class="gutterH">  15:</span>        <span class="syntax18">{</span>
    <span class="gutter">  16:</span>            <span class="syntax6">removeCloseButton</span><span class="syntax18">(</span>children[i]<span class="syntax18">)</span>;
    <span class="gutter">  17:</span>        <span class="syntax18">}</span>
    <span class="gutter">  18:</span>    <span class="syntax18">}</span>
    <span class="gutter">  19:</span><span class="syntax18">}</span>



Here are some Sun forums I've searched so far to find the possible helps for this solution:



  * [http://forum.java.sun.com/thread.jspa?threadID=630096](http://forum.java.sun.com/thread.jspa?threadID=630096)
  * [http://forum.java.sun.com/thread.jspa?threadID=690852&messageID=4016833](http://forum.java.sun.com/thread.jspa?threadID=690852&messageID=4016833)
  * [http://forum.java.sun.com/thread.jspa?forumID=54&threadID=501146](http://forum.java.sun.com/thread.jspa?forumID=54&threadID=501146)
  * [http://forum.java.sun.com/thread.jspa?threadID=356373&messageID=1486015](http://forum.java.sun.com/thread.jspa?threadID=356373&messageID=1486015)
  * [http://forum.java.sun.com/thread.jspa?threadID=5171154&messageID=9658560](http://forum.java.sun.com/thread.jspa?threadID=5171154&messageID=9658560)
  * [http://forum.java.sun.com/thread.jspa?threadID=765742&messageID=4366238](http://forum.java.sun.com/thread.jspa?threadID=765742&messageID=4366238)


Hope you make use of those tricks in your projects :-).
