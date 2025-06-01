---
id: 27
title: 'SRP Example &#8211; Bowling Game'
guid: 'http://rnaufal.wordpress.com/2006/09/18/srp-example-bowling-game/'
lj_itemid:
    - '33'
lj_permalink:
    - 'http://rnaufal.livejournal.com/8496.html'
dsq_thread_id:
    - '102765044'
categories:
    - Uncategorized
tags:
    - oop
---

Browsing Uncle Bob’s [blog](http://butunclebob.com/), I’ve found this interesting [post](http://butunclebob.com/ArticleS.UncleBob.TheBowlingGameKata) about teaching [TDD](http://en.wikipedia.org/wiki/Test_driven_development) with a practical example. It tries to show the principles of TDD while implementing a bowling game. A class diagram showing the mainly concepts of the game is presented. Here it is (click on the thumbnail to see a larger image):

[Bowling Game](http://geocities.yahoo.com.br/rsilvasp/bowling_game.html)

Some Java code of Game class is show below:

```java
public class Game {
    private int rolls[] = new int[21];
    private int currentRoll = 0;

    public void roll(int pins) {
        rolls[currentRoll++] = pins;
    }

    public int score() {
        int score = 0;
        int frameIndex = 0;
        for (int frame = 0; frame < 10; frame++) {
            if (isStrike(frameIndex)) {
                score += 10 + strikeBonus(frameIndex);
                frameIndex++;
            } else if (isSpare(frameIndex)) {
                score += 10 + spareBonus(frameIndex);
                frameIndex += 2;
            } else {
                score += sumOfBallsInFrame(frameIndex);
                frameIndex += 2;
            }
        }
        return score;
    }
    .
    .
    .
}
```

The Single Responsability Principle ([SRP](http://en.wikipedia.org/wiki/Single_responsibility_principle)) states “there should never be more than one reason for a class to change”. Analysing carefully the Game class, you can note it has more than one reason to change. So, this class has more than one responsability. One is to keep track of the current frame and the other is to calculate the score. It sometimes is hard to see beacuse it’s difficult to detect a bad class design concerning SRP, because SRP is about implementation, not interface, as I’ve [posted](http://rnaufal.livejournal.com/#rnaufal5477) before. It’s bad for a class to have two responsabilities, because they become coupled. In the real world this king of coupling doesn’t exist, so in the computational world you can’t create this coupling. If we have to change a client of the BowlingGame class who depends only on the *roll()* operation and this change causes the BowlingGame class too, we would have to rebuild and retest another client of the BowlingGame class who depends on the *score()* operation. A better design would separate these responsabilities in different classes or maybe applying Interface Segregation Principle ([ISP](http://www.objectmentor.com/resources/articles/isp.pdf)). I’ve changed a little this class design, ending up doing this (click ont the thumbnail to see a larger image):

[Bowling Game](http://geocities.yahoo.com.br/rsilvasp/bowling_game_new.html)

Notice that I have decoupled the clients from the BowlingGame in terms of interfaces. Now, those interfaces provide the clients the services they need, staying far away from the Game implementation.  
I think this class design is better beacuse we have decoupled the concepts from each other concerning the whole application, separating in two interfaces. Notice the implementation of the two responsabilities still continues in the BowlingGame  
class, but nobody need depend upon this class. Nobody will know it exists. The client who needs to know the bowling game score, will depend on the *Scorer* interface and another client who wants to register rolls will depend on the *RollRegister* interface. The implementation is far away from the client. I will change the code concerning this new design and I will post here later. As I’ve told, I think this design is better. Do you have an opinion or suggestion about this?