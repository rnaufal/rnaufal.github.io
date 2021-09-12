---
author: admin
comments: true
date: 2006-09-18 22:52:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2006/09/18/srp-example-bowling-game/
slug: srp-example-bowling-game
title: SRP Example - Bowling Game
wordpress_id: 27
tags:
- oop
---

Browsing Uncle Bob's [blog](http://butunclebob.com/), I've found this interesting [post](http://butunclebob.com/ArticleS.UncleBob.TheBowlingGameKata) about teaching [TDD](http://en.wikipedia.org/wiki/Test_driven_development) with a practical example. It tries to show the principles of TDD while implementing a bowling game. A class diagram showing the mainly concepts of the game is presented. Here it is (click on the thumbnail to see a larger image):

[![Bowling Game](http://geocities.yahoo.com.br/rsilvasp/bowling_game_thumb.jpg)](http://geocities.yahoo.com.br/rsilvasp/bowling_game.html)

Some Java code of Game class is show below:


    
    <span class="gutter">   1:</span><span class="syntax8">public</span> <span class="syntax10">class</span> Game
    <span class="gutter">   2:</span><span class="syntax18">{</span>
    <span class="gutter">   3:</span>    <span class="syntax8">private</span> <span class="syntax10">int</span> rolls[] <span class="syntax18">=</span> <span class="syntax8">new</span> <span class="syntax10">int</span> [<span class="syntax5">21</span>];
    <span class="gutter">   4:</span>    <span class="syntax8">private</span> <span class="syntax10">int</span> currentRoll <span class="syntax18">=</span> <span class="syntax5">0</span>;
    <span class="gutterH">   5:</span>
    <span class="gutter">   6:</span>    <span class="syntax8">public</span> <span class="syntax10">void</span> <span class="syntax6">roll</span>(<span class="syntax10">int</span> pins)
    <span class="gutter">   7:</span>    <span class="syntax18">{</span>
    <span class="gutter">   8:</span>        rolls[currentRoll<span class="syntax18">+</span><span class="syntax18">+</span>] <span class="syntax18">=</span> pins;
    <span class="gutter">   9:</span>    <span class="syntax18">}</span>
    <span class="gutterH">  10:</span>
    <span class="gutter">  11:</span>    <span class="syntax8">public</span> <span class="syntax10">int</span> <span class="syntax6">score</span>()
    <span class="gutter">  12:</span>    <span class="syntax18">{</span>
    <span class="gutter">  13:</span>        <span class="syntax10">int</span> score <span class="syntax18">=</span> <span class="syntax5">0</span>;
    <span class="gutter">  14:</span>        <span class="syntax10">int</span> frameIndex <span class="syntax18">=</span> <span class="syntax5">0</span>;
    <span class="gutterH">  15:</span>        <span class="syntax8">for</span>(<span class="syntax10">int</span> frame <span class="syntax18">=</span> <span class="syntax5">0</span>; frame <span class="syntax18"><</span> <span class="syntax5">10</span>; frame<span class="syntax18">+</span><span class="syntax18">+</span>) <span class="syntax18">{</span>
    <span class="gutter">  16:</span>            <span class="syntax8">if</span>(<span class="syntax6">isStrike</span>(frameIndex)) <span class="syntax18">{</span>
    <span class="gutter">  17:</span>                score <span class="syntax18">+</span><span class="syntax18">=</span> <span class="syntax5">10</span> <span class="syntax18">+</span> <span class="syntax6">strikeBonus</span>(frameIndex);
    <span class="gutter">  18:</span>                frameIndex<span class="syntax18">+</span><span class="syntax18">+</span>;
    <span class="gutter">  19:</span>            <span class="syntax18">}</span>
    <span class="gutterH">  20:</span>            <span class="syntax8">else</span> <span class="syntax8">if</span>(<span class="syntax6">isSpare</span>(frameIndex)) <span class="syntax18">{</span>
    <span class="gutter">  21:</span>                score <span class="syntax18">+</span><span class="syntax18">=</span> <span class="syntax5">10</span> <span class="syntax18">+</span> <span class="syntax6">spareBonus</span>(frameIndex);
    <span class="gutter">  22:</span>                frameIndex <span class="syntax18">+</span><span class="syntax18">=</span> <span class="syntax5">2</span>;
    <span class="gutter">  23:</span>            <span class="syntax18">}</span>
    <span class="gutter">  24:</span>            <span class="syntax8">else</span> <span class="syntax18">{</span>
    <span class="gutterH">  25:</span>                score <span class="syntax18">+</span><span class="syntax18">=</span> <span class="syntax6">sumOfBallsInFrame</span>(frameIndex);
    <span class="gutter">  26:</span>                frameIndex <span class="syntax18">+</span><span class="syntax18">=</span> <span class="syntax5">2</span>;
    <span class="gutter">  27:</span>            <span class="syntax18">}</span>
    <span class="gutter">  28:</span>        <span class="syntax18">}</span>
    <span class="gutter">  29:</span>        <span class="syntax8">return</span> score;
    <span class="gutterH">  30:</span>    <span class="syntax18">}</span>
    <span class="gutter">  31:</span>    .
    <span class="gutter">  32:</span>    .
    <span class="gutter">  33:</span><span class="syntax18">}</span>
    



The Single Responsability Principle ([SRP](http://en.wikipedia.org/wiki/Single_responsibility_principle)) states "there should never be more than one reason for a class to change". Analysing carefully the Game class, you can note it has more than one reason to change. So, this class has more than one responsability. One is to keep track of the current frame and the other is to calculate the score. It sometimes is hard to see beacuse it's difficult to detect a bad class design concerning SRP, because SRP is about implementation, not interface, as I've [posted](http://rnaufal.livejournal.com/#rnaufal5477) before. It's bad for a class to have two responsabilities, because they become coupled. In the real world this king of coupling doesn't exist, so in the computational world you can't create this coupling. If we have to change a client of the BowlingGame class who depends only on the _roll()_ operation and this change causes the BowlingGame class too, we would have to rebuild and retest another client of the BowlingGame class who depends on the _score()_ operation. A better design would separate these responsabilities in different classes or maybe applying Interface Segregation Principle ([ISP](http://www.objectmentor.com/resources/articles/isp.pdf)). I've changed a little this class design, ending up doing this (click ont the thumbnail to see a larger image):

[![Bowling Game](http://geocities.yahoo.com.br/rsilvasp/bowling_game_new_thumb.jpg)](http://geocities.yahoo.com.br/rsilvasp/bowling_game_new.html)

Notice that I have decoupled the clients from the BowlingGame in terms of interfaces. Now, those interfaces provide the clients the services they need, staying far away from the Game implementation.
I think this class design is better beacuse we have decoupled the concepts from each other concerning the whole application, separating in two interfaces. Notice the implementation of the two responsabilities still continues in the BowlingGame 
class, but nobody need depend upon this class. Nobody will know it exists. The client who needs to know the bowling game score, will depend on the _Scorer_ interface and another client who wants to register rolls will depend on the _RollRegister_ interface. The implementation is far away from the client. I will change the code concerning this new design and I will post here later. As I've told, I think this design is better. Do you have an opinion or suggestion about this?
