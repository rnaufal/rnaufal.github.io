---
id: 62
title: 'DomainDrivenDesign: Domain Services or Method on an Entity?'
date: '2008-03-31T00:50:00-03:00'
guid: 'http://rnaufal.wordpress.com/2008/03/31/domaindrivendesign-domain-services-or-method-on-an-entity/'
lj_itemid:
    - '70'
lj_permalink:
    - 'http://rnaufal.livejournal.com/18094.html'
dsq_thread_id:
    - '102734507'
categories:
    - Uncategorized
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

So, <span style="color:rgb(0,104,28);">nickgieschen</span> suggested the following C# implementations:

1\. Everything in the domain:

```csharp
class Order {
    IOrderShippedNotificationPolicy _notificationPolicy
    IOrderRepository _orderRepository
 
    void Ship() {
        if (!CheckIfOkayToShip()) {
            throw new InvalidObjectException();
        }
        UpdateQuantity();
        _orderRepository.Add(this);
        _notificationPolicy.Notify(this);
    }
}
        
class OrderShippedNotifyByEmailPolicy : INotificationPolicy {
    // The object that gets injected is implemented
    // in the infrastructure layer
    IEmailGateway _emailGateway

    void Send(Order this) {
        // Create email here
        _emailGateway.Send(email);
    }
}
```

2\. Or have an application service coordinate:

```csharp
class OrderService {
  // _orderRepository and _orderShippedNotificationPolicy
  //  are injected dependencies

  void ShipOrder(Order order) {
    order.Ship(); // in this case it only validates and updates quantity
    _orderRepository.Save(order);
    _orderShippedNotificationPolicy.Notify(order);
  }
}
```

There’s been a lot of replies also. I highlighted the interesting ones:

> “The advantage of the latter scenario is that you’re calling \_orderRepository. **Save in the application layer, which I prefer since it’s easier to see the transactional control**. The problem with the latter scenario is that it seems it’s putting **things in the application layer which don’t need to be there**. The action to `Ship()` seems to me **an atomic, domain centered action and should therefore sit in the domain**. **I consider the application layer to be like a thin domain facade as defined by [Fowler](http://martinfowler.com/)**. That is, it is only there to direct/coordinate domain activities. Like I said, `Ship()` seems like it should be considered one activity, and therefore coordination from a service layer shouldn’t be necessary.”

> “The way I look at it – what needs to go into `Ship()` is the stuff that \_must\_ happen before shipping can happen. **And shipping can happen without the notification part.** You only have a rule that says “send a notification to the customer upon shipping the order”. **You don’t have a rule that says “make sure the customer gets the notification or there are no shipments”.**

> “So, perhaps as a rough, preliminary rule we can say anything which affects the state of the domain should go be placed in the domain. (Of course, the application layer can affect the state of the domain, but only by using domain items to do so maybe think of it as the Law of Demeter among layers.) **The email doesn’t have any meaning within the domain – it’s simply a reflection of the domain.**“

> **“Notificitation of an order and the order itself is two separate concepts.”**

> **“This could as easily be implemented using AOP.”**

I think DDD advocates are a little bit extremists with some concepts, like [repository](http://martinfowler.com/eaaCatalog/repository.html). I wouldn’t have designed it on the domain layer, because I want transactional control on the application service layer. I think the domain has to deal with its particularities, not with sending email or adding things to a repository, even being decoupled of theirs implementations (the domain has a reference only to interfaces). So I prefer the latter approach. And you? What are your thoughts about this design? How would u have designed it? Everything on the domain or have an application service coordinating the activities?