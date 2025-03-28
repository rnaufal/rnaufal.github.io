---
id: 757
title: 'About patterns for handling errors in Kafka applications'
date: '2024-11-23T19:57:07-03:00'
author: rnaufal
layout: revision
guid: 'https://rafaelnaufal.com/?p=757'
---

I have just read an interesting article about [patterns for handling errors in Kafka](https://www.confluent.io/blog/error-handling-patterns-in-kafka/). The article presents four patterns for handling errors in Kafka applications:

- Stop on error
- Dead Letter Queue
- Retry topic and retry application
- Maintain order of redirected events

I have already used the `<a href="https://spring.io/projects/spring-kafka">spring-kafka</a>` [@RetryableTopic](https://docs.spring.io/spring-kafka/reference/retrytopic/retry-config.html#using-the-retryabletopic-annotation) annotation where it handles the creation of the retry and dead letter topics automatically for Java and Kotlin backend applications. It is very useful and saves a lot of time in these scenarios.

How do you handle errors in Kafka applications? Drop you comments below about what you do in these situations.