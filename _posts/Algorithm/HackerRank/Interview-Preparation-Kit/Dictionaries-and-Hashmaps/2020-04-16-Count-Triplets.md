---
layout: post
title: "[Algorithm/HackerRank] Dictionaries and Hashmaps - Count Triplets"
date: 2020-04-16 01:52:23 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Dictionaries and Hashmaps
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
You are given an array and you need to find number of tripets of indices `(i, j, k)` such that the elements at those indices are in geometric progression for a given common ratio `r` and `i < j < k`.

For example, `arr=[1, 4, 16, 64]`. If `r = 4` , we have `[1, 4, 16]` and `[4, 16, 64]` at indices `(0, 1, 2)` and `(1, 2, 3)`.

## Function Description

Complete the countTriplets function in the editor below. It should return the number of triplets forming a geometric progression for a given `r` as an integer.

countTriplets has the following parameter(s):
- arr: an array of integers
- r: an integer, the common ratio

## Input Format
The first line contains two space-separated integers `n` and `r`, the size of `arr` and the common ratio.
The next line contains `n` space-seperated integers `arr[i]`.

## Output Format
Return the count of triplets that form a geometric progression.

## Sample Input 1
```

4 2
1 2 2 4
```


## Sample Output 1
```

2
```


## Sample Input 1
```

6 3
1 3 9 9 27 81
```


## Sample Output 1
```

6
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the countTriplets function below.
def countTriplets(arr, r):
    """
    등비수열 문제
    A=1, B=3, C=9, r=3이다. 
    이때 B=A*r, C=B*r이며 A=B/r이다. 즉, B=C/r도 된다.
    여기서는 숫자 리스트 arr과 공비 r이 주어짐
    arr[i] = 임의의 숫자 k
    arr[j] = k * r
    arr[k] = k * r * r
    를 만족하는 (i, j, k)의 총 갯수를 구해야 하는 문제 
    즉 j만 알면 i, k는 알 수 있으므로
    (i, j, k) = (i = j/r, j = k*r, k = j*r) 
    """
    rDic = dict()
    lDic = dict()

    # j/r과 j*r 즉, i와 k의 수를 찾을 dictionary를 생성
    # 여기서는 k를 미리 만들어 놓음
    for n in arr:
        if n in rDic:
            rDic[n] += 1
        else:
            rDic[n] = 1
    
    count = 0
    for n in arr:
        rDic[n] -= 1

        # 반복에서 j가 되는 시점에 lDic와 rDic를 가지고 카운트
        if n%r == 0:
            if n//r in lDic and n*r in rDic:
                count += lDic[n//r] * rDic[n*r]
        
        # lDic를 안만들었으므로 lDic를 생성
        if n in lDic:
            lDic[n] += 1
        else:
            lDic[n] = 1
    
    print(count)
    return count


if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # nr = input().rstrip().split()

    # n = int(nr[0])

    # r = int(nr[1])

    # arr = list(map(int, input().rstrip().split()))

    # ans = countTriplets(arr, r)

    # fptr.write(str(ans) + '\n')

    # fptr.close()

    ans = countTriplets([1,1, 3, 3, 9], 3)

```
