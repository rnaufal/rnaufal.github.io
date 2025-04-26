---
id: 590
title: 'About the Kotlin programming language'
date: '2017-10-14T19:03:47-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=590'
dsq_thread_id:
    - '6215656980'
categories:
    - collectors
    - development
    - java
    - java8
    - kotlin
    - programming
    - streams
tags:
    - collectors
    - development
    - java
    - java8
    - kotlin
    - programming
    - streams
---

Kotlin is a statically typed language which is fully interoperable with [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

Recently my friend [Andre](https://andrematheus.net.br) showed me [Kotlin](https://kotlinlang.org/)‘s nice syntax and I considered giving it a try.

In the meantime, my friend [Leonnardo](https://github.com/leonnardo) sent me this nice [link](https://fabiomsr.github.io/from-java-to-kotlin/) which helps migrating from Java to Kotlin easily.

Let’s compare some syntax from Java and Kotlin and see the differences. Suppose we have some employees and we want to group them by their departments.

In **Java** we create an `Employee` class, build some employees and use the [Streams](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html) API to group them by their departments:

```java
public class Employee {

    private final String name;

    private final String department;

    public Employee(final String name, final String department) {
        this.name = name;
        this.department = department;
    }

    public String getName() {
        return name;
    }

    public String getDepartment() {
        return department;
    }

    @Override
    public String toString() {
        return "Employee(name=" + name + ", department=" + department + ")";
    }
}

final Employee mark = new Employee("Mark", "Accounting");
final Employee john = new Employee("John", "Management");
final Employee smith = new Employee("Smith", "Administrative");
final Employee paul = new Employee("Paul", "Accounting");

final List<Employee> employees = Arrays.asList(mark, john, smith, paul);

final Map<String, Employee> employeesByDepartment = employees
                .stream()
                .collect(Collectors.groupingBy(Employee::getDepartment));
```

In **Kotlin** we create a data class `Employee`, build some employees and use the collection built-in `groupBy` method to group them by their departments:

```kotlin
data class Employee(val name: String, val department: String)

val mark = Employee("Mark", "Accounting")
val john = Employee("John", "Management")
val smith = Employee("Smith", "Administrative")
val paul = Employee("Paul", "Accounting")

val employees = listOf(mark, john, smith, paul)

val employeesByDepartment = employees.groupBy { it.department }
```

As you can see, Kotlin has some syntactic sugar that makes it less verbose than Java.

If you haven’t considered trying Kotlin yet, I think it is worth giving it a try.