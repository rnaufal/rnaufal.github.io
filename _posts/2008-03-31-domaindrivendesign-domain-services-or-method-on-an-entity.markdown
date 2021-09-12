---
author: admin
comments: true
date: 2008-03-31 03:50:00+00:00
layout: post
link: https://rafaelnaufal.com/blog/2008/03/31/domaindrivendesign-domain-services-or-method-on-an-entity/
slug: domaindrivendesign-domain-services-or-method-on-an-entity
title: 'DomainDrivenDesign: Domain Services or Method on an Entity?'
wordpress_id: 62
tags:
- ddd
- grasp_patterns
- ooad
- patterns
- programming
---

There has been too much discussion on the [DDD](http://domaindrivendesign.org/) list regarding where to put the business logic control, whether in a service or entity. Being more specifically, in order to ship an order, the followthings should happen:



  1. Validate that the order can be shipped
  2. Update quantity
  3. Set the status to shipped
  4. Save the order
  5. Send an email to the customer that the order has been shipped
So, nickgieschen suggested the following C# implementations:

1. Everything in the domain:


    
    <span class="gutter"> 1:</span><span class="syntax10">class</span> Order
    <span class="gutter"> 2:</span><span class="syntax18">{</span>
    <span class="gutter"> 3:</span>    IOrderShippedNotificationPolicy _notificationPolicy
    <span class="gutter"> 4:</span>    IOrderRepository _orderRepository
    <span class="gutterH"> 5:</span>
    <span class="gutter"> 6:</span>    <span class="syntax10">void</span> <span class="syntax6">Ship</span>()
    <span class="gutter"> 7:</span>    <span class="syntax18">{</span>
    <span class="gutter"> 8:</span>        <span class="syntax8">if</span> (<span class="syntax18">!</span><span class="syntax6">CheckIfOkayToShip</span>()) <span class="syntax18">{</span>
    <span class="gutter"> 9:</span>            <span class="syntax8">throw</span> <span class="syntax8">new</span> <span class="syntax6">InvalidObjectException</span>();
    <span class="gutterH">10:</span>        <span class="syntax18">}</span>
    <span class="gutter">11:</span>        <span class="syntax6">UpdateQuantity</span>();
    <span class="gutter">12:</span>        _orderRepository.<span class="syntax6">Add</span>(<span class="syntax14">this</span>);
    <span class="gutter">13:</span>        _notificationPolicy.<span class="syntax6">Notify</span>(<span class="syntax14">this</span>);
    <span class="gutter">14:</span>    <span class="syntax18">}</span>
    <span class="gutterH">15:</span><span class="syntax18">}</span>
    <span class="gutter">16:</span>
    <span class="gutter">17:</span><span class="syntax10">class</span> OrderShippedNotifyByEmailPolicy : INotificationPolicy
    <span class="gutter">18:</span><span class="syntax18">{</span>
    <span class="gutter">19:</span>    <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">The</span><span class="syntax2"> </span><span class="syntax2">object</span><span class="syntax2"> </span><span class="syntax2">that</span><span class="syntax2"> </span><span class="syntax2">gets</span><span class="syntax2"> </span><span class="syntax2">injected</span><span class="syntax2"> </span><span class="syntax2">is</span><span class="syntax2"> </span><span class="syntax2">implemented</span>
    <span class="gutterH">20:</span>    <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">in</span><span class="syntax2"> </span><span class="syntax2">the</span><span class="syntax2"> </span><span class="syntax2">infrastructure</span><span class="syntax2"> </span><span class="syntax2">layer</span>
    <span class="gutter">21:</span>    IEmailGateway _emailGateway
    <span class="gutter">22:</span>    
    <span class="gutter">23:</span>    <span class="syntax10">void</span> <span class="syntax6">Send</span>(Order <span class="syntax14">this</span>)
    <span class="gutter">24:</span>    <span class="syntax18">{</span>
    <span class="gutterH">25:</span>        <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">Create</span><span class="syntax2"> </span><span class="syntax2">email</span><span class="syntax2"> </span><span class="syntax2">here</span>
    <span class="gutter">26:</span>        _emailGateway.<span class="syntax6">Send</span>(email);
    <span class="gutter">27:</span>    <span class="syntax18">}</span>
    <span class="gutter">28:</span><span class="syntax18">}</span>



2. Or have an application service coordinate:


    
    <span class="gutter">   1:</span><span class="syntax10">class</span> <span class="syntax6">OrderService</span>
    <span class="gutter">   2:</span><span class="syntax18">{</span>
    <span class="gutter">   3:</span>    <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">_orderRepository</span><span class="syntax2"> </span><span class="syntax2">and</span><span class="syntax2"> </span><span class="syntax2">_orderShippedNotificationPolicy</span><span class="syntax2"> </span>
    <span class="gutter">   4:</span>    <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2"> </span><span class="syntax2">are</span><span class="syntax2"> </span><span class="syntax2">injected</span><span class="syntax2"> </span><span class="syntax2">dependencies</span>
    <span class="gutterH">   5:</span>
    <span class="gutter">   6:</span>    <span class="syntax10">void</span> <span class="syntax6">ShipOrder</span>(Order order)
    <span class="gutter">   7:</span>    <span class="syntax18">{</span>
    <span class="gutter">   8:</span>        order.<span class="syntax6">Ship</span>(); <span class="syntax2">//</span><span class="syntax2"> </span><span class="syntax2">in</span><span class="syntax2"> </span><span class="syntax2">this</span><span class="syntax2"> </span><span class="syntax2">case</span><span class="syntax2"> </span><span class="syntax2">it</span><span class="syntax2"> </span><span class="syntax2">only</span><span class="syntax2"> </span><span class="syntax2">validates</span><span class="syntax2"> </span><span class="syntax2">and</span><span class="syntax2"> </span><span class="syntax2">updates</span><span class="syntax2"> </span><span class="syntax2">quantity</span>
    <span class="gutter">   9:</span>        _orderRepository.<span class="syntax6">Save</span>(order);
    <span class="gutterH">  10:</span>        _orderShippedNotificationPolicy.<span class="syntax6">Notify</span>(order);
    <span class="gutter">  11:</span>    <span class="syntax18">}</span>
    <span class="gutter">  12:</span><span class="syntax18">}</span>
    



There's been a lot of replies also. I highlighted the interesting ones:


<blockquote>"The advantage of the latter scenario is that you're calling _orderRepository. **Save in the application layer, which I prefer since it's easier to see the transactional control**. The problem with the latter scenario is that it seems it's putting **things in the application layer which don't need to be there**. The action to `Ship()` seems to me **an atomic, domain centered action and should therefore sit in the domain**. **I consider the application layer to be like a thin domain facade as defined by [Fowler](http://martinfowler.com/)**. That is, it is only there to direct/coordinate domain activities. Like I said, `Ship()` seems like it should be considered one activity, and therefore coordination from a service layer shouldn't be necessary."</blockquote>




<blockquote>"The way I look at it - what needs to go into `Ship()` is the stuff that _must_ happen before shipping can happen. **And shipping can happen without the notification part.** You only have a rule that says "send a notification to the customer upon shipping the order". **You don't have a rule that says "make sure the customer gets the notification or there are no shipments".**</blockquote>




<blockquote>"So, perhaps as a rough, preliminary rule we can say anything which affects the state of the domain should go be placed in the domain. (Of course, the application layer can affect the state of the domain, but only by using domain items to do so maybe think of it as the Law of Demeter among layers.) **The email doesn't have any meaning within the domain - it's simply a reflection of the domain.**"</blockquote>




<blockquote>**"Notificitation of an order and the order itself is two separate concepts."**</blockquote>




<blockquote>**"This could as easily be implemented using AOP."**</blockquote>



I think DDD advocates are a little bit extremists with some concep
ts, like [repository](http://martinfowler.com/eaaCatalog/repository.html). I wouldn't have designed it on the domain layer, because I want transactional control on the application service layer. I think the domain has to deal with its particularities, not with sending email or adding things to a repository, even being decoupled of theirs implementations (the domain has a reference only to interfaces). So I prefer the latter approach. And you? What are yout thoughts about this design? How would u have designed it? Everything on the domain or have an application service coordinating the activities?
