---
layout: post
title:  "Why scope matters, and how it can trip you up"
date:   2017-03-07 15:39:37 +0000
---

```
def team_ranker
  @teams.each do |team|
    pos = team.stats[:position]
    rank[pos.to_i - 1] = team
  end
  rank
end
```

This method was tripping me up for the longest time. I couldn't for the life of my figure out why. Let me go through it, to give a little bit of context and explain my train of thought.

We start the ```#team_ranker``` by itterating through the instance variable ```@teams```, which is an array or team objects. For each team in the array, we access the ```position``` key of the ```stats``` hash, which is the teams current ranking in the league table, and assign it to the local variable ```pos```.

The ```pos``` local variable is then used to place the team object in a new array called rank at the index corresponding to their position in the league table. The ```rank``` array is then returned.

In short, the goal here is to arrange the teams in order by their rank in order to display the league table.

I kept getting an error telling me that the rank variable was not defined... which is weird, because it clearly gets defined in order for the team objects to be added to. Cue a whole load of bindings at every stage of the loop. Sure enough, ```rank``` was defined. And sure enough, the team objects were being added to it as intended. Still, though, the error kept happening.

The solution was so simple, that I'm a little ashamed to admit how long it took for me to realise what was going on. See below

```
def team_ranker
  rank = []
  @teams.each do |team|
    pos = team.stats[:position]
    rank[pos.to_i - 1] = team
  end
	rank
end
```

```rank``` needs to be defined outside the block of the each loop, because otherwise it stops existing as soon as the loop ends.
