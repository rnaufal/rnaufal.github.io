---
id: 26
title: 'Applying the Law of Demeter'
date: '2006-09-11T00:01:00-03:00'
guid: 'http://rnaufal.wordpress.com/2006/09/11/applying-the-law-of-demeter/'
lj_itemid:
    - '32'
lj_permalink:
    - 'http://rnaufal.livejournal.com/8351.html'
dsq_thread_id:
    - '102853302'
categories:
    - Uncategorized
tags:
    - oop
---

Have you ever been told about the [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter) when developing object-oriented systems? This law states the following:

More formally, the Law of Demeter for functions requires that any method *M* of an object *O* may only invoke the methods of the following kinds of objects:

1. itself
2. its parameters
3. any objects it creates/instantiates
4. its direct component objects

In particular, an object should avoid invoking methods of a member object returned by another method.

Browsing the source code of a project, I found this Java code stretch:

```java
public class AccountHelper {

    public void creditToAccount(Account account, double value) {
        double balance = account.balance();
        double newBalance = balance + value;
        account.setBalance(newBalance);
    }

    public boolean withdrawFromAccount(Account account, double value) {
        double balance = account.balance();
        double limit = account.limit();
        double newBalance = balance;
        boolean canWithdraw = false;
        if (balance + limit >= value) {
            newBalance = balance - value;
            canWithdraw = true;
        }
        account.setBalance(newBalance);
        return canWithdraw;
    }
}
```

This code snippet doesn’t follow demeter’s law. And it’s hiding a responsability that would have been better in the *Account* class. If the *Account* knows its balance and limit, why putting the credit and withdraw behavior in a helper class? If we follow the [**Specialist**](http://rnaufal.livejournal.com/#rnaufal4963) grasp pattern, the responsability has to be at the class with the specific knowledge. So, I’ve improved the design to this new one Java code:

```java
import java.math.BigDecimal;

public class Account {
    private BigDecimal balance;
    private BigDecimal limit;

    public Account(double balance) {
        this.balance = new BigDecimal(balance);
    }

    public Account(double amount, double limit) {
        this(amount);
        this.limit = new BigDecimal(limit);
    }

    public void credit(double value) {
        balance = balance.add(new BigDecimal(value));
    }

    public boolean withdraw(double quantity) {
        if (canWithdraw(quantity)) {
            this.balance = balance.subtract(new BigDecimal(quantity));
            return true;
        }
        return false;
    }

    public double balance() {
        return balance.doubleValue();
    }

    private boolean canWithdraw(double quantity) {
        return balance.doubleValue() + limit.doubleValue() >= quantity;
    }

    public void setBalance(double balance) {
        this.balance = new BigDecimal(balance);
    }

    public double limit() {
        return limit.doubleValue();
    }
}
```

So, the initial Java code stretch become this one:

```java
public class AccountHelper {
  public void credit(Account account, double value) {
    assert account != null;
    account.credit(value);
  }

  public boolean withdraw(Account account, double value) {
    assert account != null;
    return account.withdraw(value);
  }
}
```

This code above is better because we hide from the clients the *Account* class internal structure (clients don’t need to know the existence of suborders). Moreover, if the internal structure of account is intended to change, less clients would suffer with those changes (actually, if the Account class changes, only it would have to receive the changes and its clients would have to stay far away from its changes. It’s why Object Oriented design is focused in **behavior** instead of **state**). This nice phrase resumes demeter’s law: *“The resulting software tends to be more maintainable and adaptable. Since objects are less dependent on the internal structure of other objects, object containers can be changed without reworking their callers”*.