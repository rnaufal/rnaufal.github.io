---
id: 31
title: 'List<?> or List<Object> ?'
guid: 'http://rnaufal.wordpress.com/2006/11/04/list-or-listobject/'
lj_itemid:
    - '37'
lj_permalink:
    - 'http://rnaufal.livejournal.com/9687.html'
categories:
    - Uncategorized
tags:
    - java
---

Java 1.5 introduced some new concepts at the Java language level. One of them is Generics, which you can make use mainly when creating type safe collections. This new concept facilitates the programmers’ life: being type safe, errors when working with collections can be caught at compile time (if you have a *List&lt;String&gt;*in hand, only Strings can be added to this list, neither Integers, Cats or Dogs ) and the programmer doesn’t have to cast when taking out an object of a collection. I was thus wondering whether there is any difference between *List&lt;?&gt;* and *List&lt;Object&gt;*. Let’s take a look at the following lines of Java code:

```java
import java.util.ArrayList;
import java.util.List;

public class Music {
    abstract class Instrument {}

    class Guitar extends Instrument {}

    class Flute extends Instrument {}

    class Drums extends Instrument {}

    public static void main(String[] args) {
        List<Instrument> instruments = new ArrayList<Instrument>();
        List<Guitar> guitars = new ArrayList<Guitar>();
        List<Flute> flutes = new ArrayList<Flute>();
        List<Drums> drums = new ArrayList<Drums>();
        List<Integer> integers = new ArrayList<Integer>();
        List<Object> objects = new ArrayList<Object>();
        check(instruments);
        check(guitars);
        check(flutes);
        check(drums);
        check(integers);
        validate(objects);
        validate(drums);
    }

    private static void check(List<?> instruments) {}

    private static void validate(List<Object> instruments) {}
}
```

If you try to execute the lines of code, you´ll note:

- *List&lt;?&gt;*, which is the wildcard &lt;?&gt; bounded type, also know as *List&lt;capture-of ?&gt;*, simply means “any type.” That is, it could be a List of &lt;Guitar&gt;, &lt;Flute&gt;,&lt;Drums&gt;, whatever. It also means that you cannot **ADD** anything to the list referred to as *List&lt;?&gt;*.
- *List&lt;Object&gt;* only accepts Object as an argument. Not Guitars, Drums, Flutes or Integers. If you have a method which the argument specifies *List&lt;Object&gt;*, this method can only take a *List&lt;Object&gt;*. The compiler allows you to add to the *List&lt;Object&gt;*, since you pass an Object as an argument.

So, there are differences between *List&lt;?&gt;* and *List&lt;Object&gt;*. The above code doesn´t **compile**, because an *List&lt;Drums&gt;* is being passed to a method which has a *List&lt;Object&gt;* as argument. But if you modify the method to this one:

```java
private static void validate(List<? extends Object> instruments) {}
```

The code now **compiles**!! So, we saw the behavior of *List&lt;?&gt;* and *List&lt;? extends Object&gt;* is the same! They both means “I can refer to any type of object”. But neither *List&lt;?&gt;* nor *List&lt;?&gt;* nor *List&lt;? extends Object&gt;* are the same as *List&lt;Object&gt;*. When you see code using the *wildcard notation (?)*, you can think: “this code refer to many options”. If you try to add something to a List&lt;?&gt;, the compiler won’t let you, because whether it were possible, it would be an unsafe operation, as you could pass a *List&lt;Guitar&gt;* to a method which receives a *List&lt;?&gt;* and add, say, a String to the list, as *List&lt;?&gt;* accepts “any type”. So now you may think: “Ok, Generics is a good feature, I can now create type safe collections and work with them in a safer way at compile time, that’s very good”. But everything isn’t the way we’d want it to be. If you try to mix Java generics code and legacy code,

```java
private static void add(List instruments) {
    instruments.add("45");
}
```

and

```java
add(instruments);
add(guitars);
add(flutes);
add(drums);
add(integers);
add(objects);
```

It **compiles**!! But let’s deal with it in another post.