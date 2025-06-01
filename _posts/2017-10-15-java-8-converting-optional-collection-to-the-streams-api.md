---
id: 554
title: 'Java 8: Converting Optional Collection to the Streams API'
guid: 'http://rafaelnaufal.com/blog/?p=554'
dsq_thread_id:
    - '6217518496'
categories:
    - collectors
    - development
    - idea
    - intellij
    - java
    - java8
    - jdk8
    - jdk9
    - optional
    - programming
    - streams
tags:
    - collectors
    - development
    - idea
    - intellij
    - java
    - java8
    - jdk8
    - jdk9
    - optional
    - programming
    - streams
---

Although [Java 9](http://www.oracle.com/technetwork/java/javase/downloads/index.html) has already been released, this post is about converting an optional collection to the [Streams API](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) introduced in [Java 8](http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk8-downloads-2133151.html).

Suppose some person could have zero, one or more cars and it is represented by the `Person` class below (some code omitted).

```java
public class Person {

    private String name;

    .
    .
    .

    public Optional<Collection<Car>> getCars() {
        return Optional.ofNullable(cars);
    }

    .
    .
    .

}
```

Now we create a list of people and we want to get Mark’s cars.

```java
Person mark = new Person("Mark");

List<Person> people = ...
```

How can we do that using the Streams API, since the `getCars()` method return an [Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)?

One possibility is to filter people’s list by Mark’s name, filter the `Optional` if it is present or not and map its wrapped value (our cars list):

```java
Collection<Car> markCars = people
                .stream()
                .filter(person -> "Mark".equals(person.getName()))
                .findFirst()
                .map(Person::getCars)
                .filter(Optional::isPresent)
                .map(Optional::get)
                .orElse(Collections.emptyList());
```

At this moment we reached the reason of this blog post. And how can we get all people’s cars? The idea here is to use the `flatMap()` operation unwrapping the `Optional` to the collection’s stream when it is present or getting an empty stream when it isn’t present:

```java
Collection<Car> allPeopleCars = people
                .stream()
                .map(Person::getCars)
                .flatMap(mayHaveCars -> mayHaveCars.isPresent() ? mayHaveCars.get().stream() : Stream.empty())
                .collect(Collectors.toList());
```

We can do better and replace the above solution to be more functional using [method references](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html):

```java
Collection<Car> allPeopleCars = people
                .stream()
                .map(Person::getCars)
                .flatMap(mayHaveCars -> mayHaveCars.map(Collection::stream).orElse(Stream.empty()))
                .collect(Collectors.toList());
```

If you use [IntelliJ IDEA](https://www.jetbrains.com/idea/) as your favorite IDE, it has an inspection that helps replacing `Optional.isPresent()` with a functional expression:

```java
Collection<Car> allPeopleCars = people
                .stream()
                .map(Person::getCars)
                .flatMap(mayHaveCars -> mayHaveCars.map(Collection::stream).orElseGet(Stream::empty))
                .collect(Collectors.toList());
```

**P.S.** In Java 9, the [stream()](http://download.java.net/java/jdk9/docs/api/java/util/Optional.html#stream--) method was added to the [Optional](http://download.java.net/java/jdk9/docs/api/java/util/Optional.html) API, so we can rewrite the above stream pipeline into the following one:

```java
Collection<Car> allPeopleCars = people
                .stream()
                .map(Person::getCars)
                .flatMap(Optional::stream)
                .flatMap(Collection::stream)
                .collect(Collectors.toList());
```

In case you are interested, this [post](https://blog.jetbrains.com/idea/2016/07/java-8-top-tips/) on the IntelliJ IDEA blog has some good tips when working with Java 8.