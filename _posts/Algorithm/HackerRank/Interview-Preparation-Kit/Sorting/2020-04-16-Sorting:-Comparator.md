---
layout: post
title: "[Algorithm/HackerRank] Sorting - Sorting: Comparator"
date: 2020-04-16 02:05:36 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Sorting
---

<!-- more -->


## Probleam
Comparators are used to compare two objects. In this challenge, you'll create a comparator and use it to sort an array. The Player class is provided in the editor below. It has two fields:

1. `name`: a string.
2. `score`: an integer.
Given an array of `n` Player objects, write a comparator that sorts them in order of decreasing score. If `2` or more players have the same score, sort those players alphabetically ascending by name. To do this, you must create a Checker class that implements the Comparator interface, then write an int compare(Player a, Player b) method implementing the Comparator.compare(T o1, T o2) method. In short, when sorting in ascending order, a comparator function returns `-1` if `a<b`, `0` if `a=b`, and `1` if `a>b`.

For example, given `n=3` Player objects with `Player.name, Player.score` values of `data = [[Smith, 20], [Jones, 15], [Jones, 20]]`, we want to sort the list as `data(sorted) = [[Jones, 20], [Smith, 20], [Jones, 15]]`.

## Function Description
Declare a Checker class that implements the comparator method as described. It should sort first descending by score, then ascending by name. The code stub reads the input, creates a list of Player objects, uses your method to sort the data, and prints it out properly.

## Input Format
Locked stub code in the Solution class handles the following input from stdin:

The first line contains an integer, `n`, the number of players.
Each of the next `n` lines contains a player's respective `name` and `score`, a string and an integer.

## Output Format
You are not responsible for printing any output to stdout. Locked stub code in Solution will create a Checker object, use it to sort the Player array, and print each sorted element.

## Sample Input 1
```

5
amy 100
david 100
heraldo 50
aakansha 75
aleksa 150
```


## Sample Output 1
```

aleksa 150
amy 100
david 100
aakansha 75
heraldo 50
```


## Code

```python
from functools import cmp_to_key
class Player:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def comparator(a, b):
        """
        스코어를 기준으로 내림차순 대신 스코어가 같다면 이름은 오른차순
        """
        if a.score == b.score: # 스코어가 같다면
            
            # 이름은 오름차순이므로 (x - y == 1)가 성립하기 위해
            # a.name 즉 x가 더 큰 경우에만 1이라는 것이 오름차순이므로..
            if a.name > b.name:
                return 1
            else:
                return -1
        else:
            # 스코어는 내림차순 y - x
            return b.score - a.score

n = int(input())
data = []
for i in range(n):
    name, score = input().split()
    score = int(score)
    player = Player(name, score)
    data.append(player)
    
data = sorted(data, key=cmp_to_key(Player.comparator))
for i in data:
    print(i.name, i.score)
```
