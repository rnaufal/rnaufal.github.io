---
id: 69
title: 'Bean Validation – Emmanuel Bernard on JSR 303'
date: '2009-03-22T14:57:00-03:00'
guid: 'http://rnaufal.wordpress.com/2009/03/22/bean-validation-%e2%80%93-emmanuel-bernard-on-jsr-303/'
lj_itemid:
    - '78'
lj_permalink:
    - 'http://rnaufal.livejournal.com/20015.html'
dsq_thread_id:
    - '102751733'
categories:
    - Uncategorized
tags:
    - bean
    - framework
    - java
    - programming
---

[JavaLobby](http://java.dzone.com/articles/bean-validation-rest-us-%E2%80%93) released an interesting interview with Emmanuel Bernard, the spec lead of *of JSR-303: Bean Validation.*.

One of the important goals of the Bean Validation spec is, as Emmanuel Bernard says, is

> to provide a default runtime engine that is used to validate the constraints around the domain model, in Java.

The development team decided to use annotations to express the constraints applied at the domain model. They argued that with annotations the constraints are put directly at the properties in the code, expressing the constraints associated with the property.

I highlighted some interesting parts of the interview:

> Bean Validation lets you **standardize the way you declare the constraints.** So an application developer will just know one way to declare constraints, and just forget about all the different models. There’s no duplication around the validation on the layers.

> If you think about a constraint, a **constraint is really some kind of an extension of the type system**.

> Bean Validation lets you validate an object graph using the @**Valid** annotation. Basically saying, ‘Well, when you validate this object, make sure the associated object is validated as well.’ By the way, **even if Bean Validation is primarily annotation focused, there is the equivalent in XML**.

> Any framework that is having a need to use validation, to apply validation, can either use the runtime engine of Bean Validation or go extract the **metadata** and play with that. So the user declares it once, in one place, and every framework in the Java space can actually go and either apply the validation routine …

You can listen the podcast of the interview also. It’s very noteworthy to read or listen the interview and see what’s next on validation in Java. Before the Bean Validation API become public to all of us, which framework do you use to validate constraints on the Java platform?