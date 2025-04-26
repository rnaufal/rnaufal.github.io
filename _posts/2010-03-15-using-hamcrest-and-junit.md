---
id: 218
title: 'Using Hamcrest and JUnit'
date: '2010-03-15T23:10:52-03:00'
guid: 'http://rafaelnaufal.com/blog/?p=218'
dsq_thread_id:
    - '76180944'
categories:
    - Uncategorized
tags:
    - google
    - hamcrest
    - java
    - junit
    - matchers
    - testing
    - tests
---

Lately I started using the core [Hamcrest](http://junit.sourceforge.net/doc/ReleaseNotes4.4.html) matchers bundled with the JUnit framework to create more readable unit tests.

Hamcrest matchers were created to improve the readability of unit testing code. It’s a framework which facilitates the creation of *matcher* objects to match rules specified in unit tests. Some examples will let it to be clearer:

```java
import static org.hamcrest.CoreMatchers.equalTo;
import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertThat;

@Test
public void shouldBeTheSamePerson() {
    Person me = new Person("Rafael");
    Person theOther = new Person("Rafael");
    assertThat(me, is(theOther));
}

@Test
public void shouldHaveFixedSizeNumbers() {
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    assertThat(numbers.size(), is(equalTo(5)));
}
```

The first example checks if one `Person` object is equal to another using the `Object equals `method, which was overridden in the `Person` class. The `is` syntax defines a matcher which is a shorthand to `is(equalTo(value))`. The second one uses the `is(equalTo(value))` matcher to check the size of an integer list of fixed size numbers. The `assertThat` method is used in conjunction with the `is(equalTo(value))` matcher, which makes the test sentence very human readable.

An interesting thing is the possibility to create a custom matcher, like this one which tests if a given list only has even numbers:

```java
public class AreEvenNumbers extends TypeSafeMatcher<Collection<Integer>> {

  @Override
  public boolean matchesSafely(Collection<Integer> numbers) {
    for (Integer number : numbers) {
      if (number % 2 != 0) {
        return false;
      }
    }
    return true;
  }

  @Override
  public void describeTo(Description description) {
    description.appendText("even numbers");
  }

  @Factory
  public static <T> Matcher<Collection<Integer>> evenNumbers() {
    return new AreEvenNumbers();
  }
}
```

And below are two tests which uses the `AreEvenNumbers` custom matcher:

```java
import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertThat;
import static br.com.rafael.hamcrest.AreEvenNumbers.evenNumbers;

@Test
public void shouldHaveOnlyEvenNumbers() {
    List<Integer> numbers = Arrays.asList(2, 4, 6, 8, 10);
    assertThat(numbers, is(evenNumbers()));
}

@Test
public void shouldNotHaveOddNumbers() {
    List<Integer> numbers = Arrays.asList(1, 2, 4, 6, 8, 10);
    assertThat(numbers, not(evenNumbers()));
}
```

These two tests use the static factory method `evenNumbers` to instantiate the matcher on the test code. Not the use of the `not` matcher on the `shouldNotHaveOddNumbers` test to assert that no odd numbers are present on the given list. All tests use the [static import](http://java.sun.com/j2se/1.5.0/docs/guide/language/static-import.html) feature, which turns the test not clean and not cluttered with the class qualification.

I haven’t experienced the other common matchers on unit testing code, like the Beans, Collections and Number ones. I think they turn the tests more readable, clean and easy to change. And you? Have you ever used Hamcrest matcher? If you have other examples of using it, post them here!

***Updated:** Static imports were added to the testing code.*