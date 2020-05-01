---
layout: post
title: "[Algorithm/HackerRank] Sorting - Mark and Toys"
date: 2020-04-16 02:01:48 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Sorting
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
Mark and Jane are very happy after having their first child. Their son loves toys, so Mark wants to buy some. There are a number of different toys lying in front of him, tagged with their prices. Mark has only a certain amount to spend, and he wants to maximize the number of toys he buys with this money.

Given a list of prices and an amount to spend, what is the maximum number of toys Mark can buy? For example, if `prices=[1, 2, 3, 4]` and Mark has `k=7` to spend, he can buy items `[1, 2, 3]` for `6`, or `[3,4]` for `7` units of currency. He would choose the first group of `3` items.

## Function Description
Complete the function maximumToys in the editor below. It should return an integer representing the maximum number of toys Mark can purchase.

maximumToys has the following parameter(s):

- prices: an array of integers representing toy prices
- k: an integer, Mark's budget

## Input Format
The first line contains two integers, `n` and `k`, the number of priced toys and the amount Mark has to spend.
The next line contains `n` space-separated integers `prices[i]`

## Output Format
An integer that denotes the maximum number of toys Mark can buy for his son.

### Sample Input 1
```

7 50
1 12 5 111 200 1000 10
```


### Sample Output 1
```

4
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the maximumToys function below.
def maximumToys(prices, k):
    
    arr = sorted(prices)
    count = 0
    for i in arr:
        if (k-i) > 0:
            count += 1
            k -= i

    return count

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nk = input().split()

    n = int(nk[0])

    k = int(nk[1])

    prices = list(map(int, input().rstrip().split()))

    result = maximumToys(prices, k)

    fptr.write(str(result) + '\n')

    fptr.close()
```
