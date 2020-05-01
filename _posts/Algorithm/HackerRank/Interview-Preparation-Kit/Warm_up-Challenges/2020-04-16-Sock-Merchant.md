---
layout: post
title: "[Algorithm/HackerRank] Warm_up Challenges - Sock Merchant"
date: 2020-04-16 01:19:37 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Warm_up Challenges
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
John works at a clothing store. He has a large pile of socks that he must pair by color for sale. Given an array of integers representing the color of each sock, determine how many pairs of socks with matching colors there are.

For example, there are `n=7` socks with colors `ar=[1, 2, 1, 2, 1, 3, 2]`. There is one pair of color `1` and one of color `2`. There are three odd socks left, one of each color. The number of pairs is `2`.

## Function Description
Complete the sockMerchant function in the editor below. It must return an integer representing the number of matching pairs of socks that are available.

sockMerchant has the following parameter(s):

- n: the number of socks in the pile
- ar: the colors of each sock

## Input Format
The first line contains an integer `n`, the number of socks represented in `ar`.
The second line contains `n` space-separated integers describing the colors `ar[i]` of the socks in the pile.

## Output Format
Return the total number of matching pairs of socks that John can sell.

## Sample Input
```

9
10 20 20 10 10 30 50 10 20
```


## Sample Output
```

3
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the sockMerchant function below.
def sockMerchant(n, ar):
    """
    :param n: int
    :param ar: list
    :return: int
    """

    temp = []    # ar에 들어오는 중복값의 카운트 처리를 위한 배열 변수
    total = 0    # 카운트가 더해질 변수

    for i in range(n):
        sock = ar[i] # 양말
        
        # 한 쌍이되는 양말 수량 카운트
        if not sock in temp:
            temp.append(sock)
        else:
            total = total + 1
            temp.remove(sock)

    return total

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    ar = list(map(int, input().rstrip().split()))

    result = sockMerchant(n, ar)

    fptr.write(str(result) + '\n')

    fptr.close()

```
