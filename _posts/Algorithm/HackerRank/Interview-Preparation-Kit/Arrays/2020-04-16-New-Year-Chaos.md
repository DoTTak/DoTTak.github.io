---
layout: post
title: "[Algorithm/HackerRank] Arrays - New Year Chaos"
date: 2020-04-16 01:39:13 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Arrays
toc: true
---

<!-- more -->


## Probleam
It's New Year's Day and everyone's in line for the Wonderland rollercoaster ride! There are a number of people queued up, and each person wears a sticker indicating their initial position in the queue. Initial positions increment by `1` from `1` at the front of the line to `n` at the back.

Any person in the queue can bribe the person directly in front of them to swap positions. If two people swap positions, they still wear the same sticker denoting their original places in line. One person can bribe at most two others. For example, if `n=8` and `Person 5` bribes `Person 4`, the queue will look like this: `1, 2, 3, 5, 4, 6, 7, 8`.

Fascinated by this chaotic queue, you decide you must know the minimum number of bribes that took place to get the queue into its current state!

## Function Description
Complete the function minimumBribes in the editor below. It must print an integer representing the minimum number of bribes necessary, or Too chaotic if the line configuration is not possible.

minimumBribes has the following parameter(s):

- q: an array of integers

## Input Format
The first line contains an integer `t`, the number of test cases.

Each of the next `t` pairs of lines are as follows:
- The first line contains an integer `t`, the number of people in the queue
- The second line has `n` space-separated integers describing the final state of the queue.

## Output Format
Print an integer denoting the minimum number of bribes needed to get the queue into its final state. Print Too chaotic if the state is invalid, i.e. it requires a person to have bribed more than `2` people.

## Sample Input 1
```

2
5
2 1 5 3 4
5
2 5 1 3 4
```


## Sample Output 1
```

3
Too chaotic
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the minimumBribes function below.
def minimumBribes(q):

    # Hint: 1~5 Sequence Integer
    # 1 2 3 4 5 순서에서 각 자리는 2칸 이상을 넘어갈 수 없다
    # 즉, 5가 2 앞으로 올 수 없음 -> 1, 5, 2, 3, 4
    # 그리고 정렬된 순서가아닌 새치기를 한 순서 이므로 앞자리가 뒷자리보다 큼
    for i in range(len(q)):
        if q[i] - i > 3:
            print("Too chaotic")
            return 0
    swap_cnt = 0
    """
    뇌물을 주고 한칸씩 이동 -> 버블정렬
    """
    for i in range(len(q)-1):
        is_swap = False
        for j in range(len(q)-1-i):
            temp = 0
            if q[j] > q[j+1]:
                temp = q[j]
                q[j] = q[j+1]
                q[j+1] = temp

                swap_cnt +=1    # swap 카운트
                is_swap = True  # swap 여부를 확인하는 이유는 바뀌지 않았다면
                                # 이미 정렬된 순서이므로 Timeout에 걸리지 않기 위함.
        
        if not is_swap:
            break

    print(swap_cnt)
            

if __name__ == '__main__':
    t = int(input())

    for t_itr in range(t):

        n = int(input())
        q = list(map(int, input().rstrip().split()))

        minimumBribes(q)
```
