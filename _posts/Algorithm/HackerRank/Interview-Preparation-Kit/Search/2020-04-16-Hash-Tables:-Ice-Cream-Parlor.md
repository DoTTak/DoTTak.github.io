---
layout: post
title: "[Algorithm/HackerRank] Search - Hash Tables: Ice Cream Parlor"
date: 2020-04-16 03:56:49 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Search
toc: true
---

<!-- more -->


## Probleam
Each time Sunny and Johnny take a trip to the Ice Cream Parlor, they pool their money to buy ice cream. On any given day, the parlor offers a line of flavors. Each flavor has a cost associated with it.

Given the value of `money` and `cost` the of each flavor for `t` trips to the Ice Cream Parlor, help Sunny and Johnny choose two distinct flavors such that they spend their entire pool of money during each visit. ID numbers are the 1- based index number associated with a `cost`. For each trip to the parlor, print the ID numbers for the two types of ice cream that Sunny and Johnny purchase as two space-separated integers on a new line. You must print the smaller ID first and the larger ID second.

For example, there are `n=5` flavors having `cost = [2,1,3,5,6]`. Together they have `money = 5` to spend. They would purchase flavor ID's `1` and `3` for a cost of `2 + 3 = 5`. Use `1` based indexing for your response.

**Note:**
- Two ice creams having unique IDs `i` and `j` may have the same cost (i.e.,`cost[i] ☰ cost[j]`).
- There will always be a unique solution.

## Function Description
Complete the function whatFlavors in the editor below. It must determine the two flavors they will purchase and print them as two space-separated integers on a line.

whatFlavors has the following parameter(s):
- cost: an array of integers representing price for a flavor
- money: an integer representing the amount of money they have to spend

## Input Format
The first line contains an integer, `t`, the number of trips to the ice cream parlor.

Each of the next `t` sets of `3` lines is as follows:
- The first line contains `money`.
- The second line contains an integer, `n`, the size of the array `cost`.
- The third line contains  space-separated integers denoting the `cost[i]`.

## Output Format
Print two space-separated integers denoting the respective indices for the two distinct flavors they choose to purchase in ascending order. Recall that each ice cream flavor has a unique ID number in the inclusive range from `1` to `|cost|`.

## Sample Input 1
```

2
4
5
1 4 5 3 2
4
4
2 2 4 3
```


## Sample Output 1
```

1 4
1 2
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the whatFlavors function below.
def whatFlavors(cost, money):
    """
    N개의 아이스크림중에서 각기 다른 2개를 골라 주어진 money와 2개의 아이스크립 비용의 합이 일치
    -> 2개의 아이스크림의 비용 == money
    """

    """
    O(n^2) 풀이
    -> 문제 풀이시 Timeout에 걸림
    """
    # for i in range(0, len(cost)):
    #     for j in range(i+1, len(cost)): # 각기 다른 아이스크림이여야 하므로 j는 i+1 처리
    #         if money - cost[i] == cost[j]:
    #             print(i+1, j+1) # +1을 한 이유는 idx가 1부터 시작하기 때문
    #             return 0
    

    """
    O(n) 풀이
    -> 조건 자체가 서로다른 아이스크림 2개의 가격이 가지고 있는 금액과 일치함
    -> 1번 째 ~ n번 째 아이스크림 비용을 순환하여 순환 시 가지고 있는 
       금액 - n번 째 아이스크림 가격이 있으면 출력 없으면 key로 등록함
    """
    cost_dict = {}
    
    for i in range(len(cost)):
        ice_id = i         # 아이스크림 ID
        ice_cost = cost[i] # 아이스크림 비용
        
        if money - ice_cost in cost_dict:
            # 나머지 아이스크림 구매 가능 금액을 찾으려면 cost_dict에서 찾으면 된다.
            print(cost_dict[money-ice_cost]+1, ice_id+1) # idx가 1부터 시작
            break
        else:
            # 아이스크림 비용을 key로 둔 dict 생성
            cost_dict[ice_cost] = ice_id

if __name__ == '__main__':
    # t = int(input())

    # for t_itr in range(t):
        # money = int(input())

        # n = int(input())

        # cost = list(map(int, input().rstrip().split()))

    whatFlavors([1, 4, 5, 3, 2], 4)
```
