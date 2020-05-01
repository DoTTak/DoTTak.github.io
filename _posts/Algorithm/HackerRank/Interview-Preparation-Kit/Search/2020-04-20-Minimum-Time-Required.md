---
layout: post
title: "[Algorithm/HackerRank] Search - Minimum Time Required"
date: 2020-04-20 03:04:14 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Search
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
You are planning production for an order. You have a number of machines that each have a fixed number of days to produce an item. Given that all the machines operate simultaneously, determine the minimum number of days to produce the required order.

For example, you have to produce `goal=10` items. You have three machines that take `machines = [2,3,2]` days to produce an item. The following is a schedule of items produced:
```

Day Production  Count
2   2               2
3   1               3
4   2               5
6   3               8
8   2              10
```

It takes `8` days to produce `10` items using these machines.

## Function Description
Complete the minimumTime function in the editor below. It should return an integer representing the minimum number of days required to complete the order.

minimumTime has the following parameter(s):
- machines: an array of integers representing days to produce one item per machine
- goal: an integer, the number of items required to complete the order


## Input Format
The first line consist of two integers `n` and `goal`, the size of `machines` and the target production.
The next line contains `n` space-separated integers, `machines[i]`.

## Output Format
Return the minimum time required to produce `goal` items considering all machines work simultaneously.

## Sample Input 1
```

2 5
2 3
```


## Sample Output 1
```

6
```


## Explanation 1
In `6` days `machine 0` can produce `3` items and `machine 1` can produce `2` items. This totals up to `5`.

## Code

```python
 #!/bin/python3

import math
import os
import random
import re
import sys

# Complete the minTime function below.
def minTime(machines, goal):
    """
    machines배열의 각각의 요소는 제품 하나를 만드는데 몇일 걸리는지 알려준다.
    goal은 목표 제품 갯수이며 goal에 도달하기 위해 최소 몇일이 걸리는지 구하는 문제이다.
    """

    # Solutions 1 -> Timeout
    """
    [1, 3, 4] -> 1일 1개, 3일 1개, 4일 1개이다. 
           1 3 4
    day-0  0 0 0
    day-1  1 0 0
    day-2  2 0 0
    day-3  3 1 0
    day-4  4 1 1
    day-5  5 1 1
    day-6  6 2 1
    day-7  7
    ------------
        7+2+1 = 10(goal)
    """
    # is_run = True
    # count = 0
    # day = 1
    # while is_run:
    #     for m in machines:
    #         if day % m == 0:
    #             count += 1
    #             if count >= goal:
    #                 is_run = False
    #                 break
    #     if is_run:
    #         day += 1

    # return day

    # Solutions 2
    machines = sorted(machines)
    print(machines, goal)
    num_machines = len(machines)
    
    # 모든 기계가 제품 1개를 만드는데 1일씩 소요된다면 목표 제품 갯수까지 가장 빠른 날 
    earliest_day = math.ceil(goal/num_machines)
    
    # 목표까지 도달하는데 걸리는 일수
    low = earliest_day * machines[0]    # 제일 빨리 만드는 머신의 날짜가 모든 머신과 같을 때 
    high = earliest_day * machines[-1]  # 제일 늦게 만드는 머신이 날짜가 모든 머신과 같을 때 

    while low < high:
        
        # 중간 값
        guess_day = (low + high) // 2

        total = 0
        for m in machines:
            total += guess_day // m
        """
        여기가 제일 중요하다.
        """
        if total >= goal:
            high = guess_day
        else:
            low = guess_day + 1

    return low

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # nGoal = input().split()

    # n = int(nGoal[0])

    # goal = int(nGoal[1])

    # machines = list(map(int, input().rstrip().split()))

    # ans = minTime(machines, goal)
    ans = minTime([1, 3, 4], 7)
    # ans = minTime([4, 5, 6], 12)

    # fptr.write(str(ans) + '\n')

    # fptr.close()

```
