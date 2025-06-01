---
id: 424
title: 'JavaCodeKata &#8211; Lambdas'
guid: 'http://rafaelnaufal.com/blog/?p=424'
dsq_thread_id:
    - '3707200815'
categories:
    - development
    - java
    - jdk8
    - kata
    - lambdas
    - programming
    - stream
---

I’ve came across that [kata](https://github.com/JavaCodeKata/stream-lambda "Lambdas") from [@brjavaman](https://twitter.com/brjavaman "brjavaman") and [@yanaga](https://twitter.com/yanaga "yanaga") to teach lambdas, one of the new features of [JDK 8](http://www.oracle.com/technetwork/java/javase/8-whats-new-2157071.html).

There are some [unit tests](http://junit.org/) to validate the solution. I’ve found it a good opportunity to exercise the use of lambdas so I decided to solve it. Below is my solution to this kata.

The first method should take the String list and sort all the String elements in ascending (ASCII) order:

```java
    /**
     * This method should take the String List and sort all the String elements in ascending (ASCII) order.
     *
     * @return The sorted values in ascending ASCII order.
     */
    public List<string> getSortedStrings() {
        return values
                .stream()
                .sorted()
                .collect(Collectors.toList());
    }
```

The other method should take the String list and:

1. filter the elements that contains one or more digits
2. transform (map) the remaining Strings into Integers
3. sort the Integers in ascending order

```java
    /**
     * This method should take the String List and:
     * <ol>
     * <li>filter the elements that contains one or more digits;</li>
     * <li>transform (map) the remaining Strings into Integers;</li>
     * <li>sort the Integers in ascending order.</li>
     * </ol>
     *
     * @return
     */
    public List<integer> getSortedIntegers() {
        return values
                .stream()
                .filter(s -> s.matches("\\d+"))
                .map(Integer::valueOf)
                .sorted()
                .collect(Collectors.toList());
    }
```

The last method should take the String list and:

1. filter the elements that contains one or more digits
2. transform (map) the remaining Strings into Integers
3. sort the Integers in descending order

```java
    /**
     * This method should take the String List and:
     * <ol>
     * <li>filter the elements that contains one or more digits;</li>
     * <li>transform (map) the remaining Strings into Integers;</li>
     * <li>sort the Integers in descending order.</li>
     * </ol>
     *
     * @return
     */
    public List<integer> getSortedDescendingIntegers() {
        return values
                .stream()
                .filter(s -> s.matches("\\d+"))
                .map(Integer::valueOf)
                .sorted(Comparator.reverseOrder())
                .collect(Collectors.toList());
    }
```

Note that the steps `filter the elements that contains one or more digits` and `transform (map) the remaining Strings into Integers` are identical. So I decided to extract the partial [Stream](http://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html "Stream") into a method with the [Extract Method](http://refactoring.com/catalog/extractMethod.html "Extract Method") refactoring support on [IntelliJ IDEA](https://www.jetbrains.com/idea/ "IntelliJ IDEA"):

```java
    private Stream<integer> integersWithOneOrMoreDigits() {
        return values
                .stream()
                .filter(s -> s.matches("\\d+"))
                .map(Integer::valueOf);
    }
```

Then I refactored the the solution to use the new extracted method:

```java
    public List<integer> getSortedIntegers() {
        return integersWithOneOrMoreDigits()
                .sorted()
                .collect(Collectors.toList());
    }
```

```java
    public List<integer> getSortedDescendingIntegers() {
        return integersWithOneOrMoreDigits()
                .sorted(Comparator.reverseOrder())
                .collect(Collectors.toList());
    }
```

I re-run the tests and they all passed. What do you think about this solution? Do you suggest other ones?