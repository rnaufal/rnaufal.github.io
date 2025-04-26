---
id: 24
title: 'Single Responsability Principle'
date: '2006-08-15T23:06:00-03:00'
guid: 'http://rnaufal.wordpress.com/2006/08/15/single-responsability-principle/'
lj_itemid:
    - '21'
lj_permalink:
    - 'http://rnaufal.livejournal.com/5477.html'
dsq_thread_id:
    - '76181466'
categories:
    - Uncategorized
tags:
    - ooad
---

Look at these [Java](http://java.sun.com) code snippet:

```java
import java.util.Date;
class Movie
{
    private Date exhibitionDate;
    private Director director;
    private Persister persister = new Persister();

    public boolean isDirectedBy(String director) {
        // some code here;
    }

    public void changeDateWithDirectorApproval(Date newDate) {
        // some code here;
    }

    public void save() {
        persister.save(this);
    }
}
```

At the *save()* method, *persister* takes care of the responsability to update the current movie, saving it at the persistent environment (a file, a DBMS, any data source, etc..) . Some may argue this class has two responsabilities: the Movie is responsible for its own behaviour AND its persistence. [ButUncleBob](http://butunclebob.com/ArticleS.DavidChelimsky.MattersOfPrinciple.SrpIsAboutImplementation) has an interesting opinion about the *Single Responsability Principle (SRP)*. It says *Movie* actually is not implementing persistence, the persister is a collaborator of the class. The persister is hidden from the client of the class, that is, is not part of the public interface. So, the lose coupling and the encapsulation is preserved. If the persister changes, the clients won’t be affected. It concludes *SRP is about implementation, not interface*. But imagine if you wanna find a movie, you can’t do movie.find() 🙂 . So, you have to deal with another collaborator who knows how to find a movie. Couldn’t be the *Persister*? No, because this one is hidden from the clients and if you become it public, you would fail with the [information hiding](http://en.wikipedia.org/wiki/Information_hiding) principle. In this case, I think it’s better a [Finder](http://www.martinfowler.com/eaaCatalog/registry.html) object. And you?