---
layout: post
title: "[Algorithm/HackerRank] Arrays - Array Manipulation"
date: 2020-04-16 01:43:57 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Arrays
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
Starting with a 1-indexed array of zeros and a list of operations, for each operation add a value to each of the array element between two given indices, inclusive. Once all operations have been performed, return the maximum value in your array.

For example, the length of your array of zeros `n=10`. Your list of queries is as follows:
```

    a b k
    1 5 3
    4 8 7
    6 9 1
```

Add the values of  between the indices  and  inclusive:
```

index->	 1 2 3  4  5 6 7 8 9 10
	[0,0,0, 0, 0,0,0,0,0, 0]
	[3,3,3, 3, 3,0,0,0,0, 0]
	[3,3,3,10,10,7,7,7,0, 0]
	[3,3,3,10,10,8,8,8,1, 0]
```
    
The largest value is `10` after all operations are performed.

## Function Description
Complete the function arrayManipulation in the editor below. It must return an integer, the maximum value in the resulting array.

arrayManipulation has the following parameters:

- n - the number of elements in your array
- queries - a two dimensional array of queries where each queries[i] contains three integers, a, b, and k.

## Input Format
The first line contains two space-separated integers `n` and `m`, the size of the array and the number of operations.
Each of the next `m` lines contains three space-separated integers `a`, `b` and `k`, the left index, right index and summand.

## Output Format
Return the integer maximum value in the finished array.

## Sample Input 1
```

5 3
1 2 100
2 5 100
3 4 100
```


## Sample Output 1
```

200
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the arrayManipulation function below.
def arrayManipulation(n, queries):
    
    # Prefix Sum(누적합) 문제
    # https://youngchangoon.tistory.com/51 참고

    arr = [0] * (n+1)

    """
    시작점과 끝점을 이용해서 최댓값을 구함.
    a~b 사이에 K의 값이 합해질 경우
    a(시작점)에 K를 합하고 b(끝점)에 K를 뺌
    이후 1~n을 합하여 최댓값을 구함
    """
    for query in queries:
        start = query[0]-1 # 주어진 문항에서는 1부터 시작하지만 실제 배열에서는 0부터 시작하므로
        end = query[1]
        add_num = query[2]

        arr[start] += add_num
        arr[end] += (-1 * add_num)

    total = 0
    max_num = 0

    for i in arr:
        total += i
        if max_num < total:
            max_num = total

    return max_num

if __name__ == '__main__':

    nm = input().split()

    n = int(nm[0])

    m = int(nm[1])

    queries = []

    for _ in range(m):
        queries.append(list(map(int, input().rstrip().split())))

    result = arrayManipulation(n, queries)
    print(result)
```
