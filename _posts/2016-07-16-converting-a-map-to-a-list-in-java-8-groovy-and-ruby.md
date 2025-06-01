---
id: 459
title: 'Converting a Map to a List in Java 8, Groovy and Ruby'
guid: 'http://rafaelnaufal.com/blog/?p=459'
dsq_thread_id:
    - '4993151356'
categories:
    - arrays
    - groovy
    - java
    - java8
    - lambdas
    - programming
    - ruby
tags:
    - closure
    - collectors
    - groovy
    - java
    - java8
    - lambdas
    - ruby
    - streams
---

Some days ago I was developing a task on a Gradle project and I faced with a situation where I had to convert a Map &lt; String, List &lt; String &gt;&gt; to List &lt; Pair &gt;, each pair containing the key and one element from the List&lt;String&gt;.

I decided to compare the solution in three different languages: [Java 8](http://docs.oracle.com/javase/8/docs/technotes/guides/language/enhancements.html#javase8) (using lambdas and the Streams API), [Groovy](http://www.groovy-lang.org/) and [Ruby](https://www.ruby-lang.org/en/) to see how concise and expressive they would be. Then, I created the Groovy code and it looked like this:

```groovy
#!/usr/bin/env groovy

def map = ["a" : ["1", "2", "3"], "b" : ["4", "5", "6"], "c" : ["7"]]

println map.collectMany { key, values -> values.collect {value -> [key, value]}}
```

Running the above code, the result is below:

```groovy
[[a, 1], [a, 2], [a, 3], [b, 4], [b, 5], [b, 6], [c, 7]]
```

The Ruby version looked like this:

```ruby
#!/usr/bin/env ruby

map = { "a" => ["1", "2", "3"], "b" => ["4", "5", "6"], "c" => ["7"] }

p map.collect {|key, values| values.map {|value| [key, value] } }.flatten(1)
```

The Ruby program generated the following output:

```ruby
[["a", "1"], ["a", "2"], ["a", "3"], ["b", "4"], ["b", "5"], ["b", "6"], ["c", "7"]]
```

Below is the Java 8 version, using lambdas, [Streams](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) and the [Collectors](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html) API:

```java
Map<String, List<String>> values = new HashMap<>();
values.put("a", Arrays.asList("1", "2", "3"));
values.put("b", Arrays.asList("4", "5", "6"));
values.put("c", Collections.singletonList("7"));

final List<Pair> result = values
        .entrySet()
        .stream()
        .collect(ArrayList::new,
                (pairs, entry) -> pairs.addAll(entry
                        .getValue()
                        .stream()
                        .map(value -> new Pair(entry.getKey(), value))
                        .collect(Collectors.toList())),
                List::addAll);

private static class Pair {

    private final String first;
    private final String second;

    public Pair(String first, String second) {
        this.first = first;
        this.second = second;
    }

    @Override
    public String toString() {
        return "Pair{first='" + first + "', second='" + second + "'}";
    }
}
```

Running the Java 8 version produced the following output:

```java
[Pair{first='a', second='1'}, Pair{first='a', second='2'}, 
Pair{first='a', second='3'}, Pair{first='b', second='4'}, 
Pair{first='b', second='5'}, Pair{first='b', second='6'}, 
Pair{first='c', second='7'}]
```

The Groovy and Ruby version are very expressive and concise. Note the use of the [collectMany](http://docs.groovy-lang.org/latest/html/groovy-jdk/java/lang/Iterable.html#collectMany(groovy.lang.Closure)) method on the Groovy version and the use of the [flatten](http://ruby-doc.org/core-2.3.1/Array.html#method-i-flatten) method on the Ruby version to flatten the result list into a single list of pairs.  
The Java 8 version made use of the [collect](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#collect-java.util.function.Supplier-java.util.function.BiConsumer-java.util.function.BiConsumer-) method of the Stream API, to collect the results in a list of `Pair` instances, each one holding the key and value of each element from the List&lt;String&gt;.

What do you think about this comparison? Leave your comments here!