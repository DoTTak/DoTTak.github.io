---
layout: post
title: "[Algorithm/HackerRank] Dynamic Programming - Abbreviation"
date: 2020-04-24 09:01:29 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Dynamic Programming
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
You can perform the following operations on the string, `a`:
1. Capitalize zero or more of `a`'s lowercase letters.
2. Delete all of the remaining lowercase letters in `a`.

Given two strings, `a` and `b`, determine if it's possible to make `a` equal to `a` as described. If so, print YES on a new line. Otherwise, print NO.

For example, given `a = AbcDE` and `b = ABDE`, in `a` we can convert `b` and delete `c` to match `b`. If `a = AbcDE` and `b = AFDE`, matching is not possible because letters may only be capitalized or discarded, not changed.

## Function Description
Complete the function `abbreviation` in the editor below. It must return either `YES` or `NO`.
abbreviation has the following parameter(s):
- a: the string to modify
- b: the string to match

## Input Format
The first line contains a single integer `q`, the number of queries.

Each of the next `q` pairs of lines is as follows:
- The first line of each query contains a single string, `a`.
- The second line of each query contains a single string, `b`.

## Output Format
For each query, print YES on a new line if it's possible to make string `a` equal to string `b`. Otherwise, print NO.

## Sample Input 1
```

1
daBcd
ABC
```


## Sample Output 1
```

YES
```


## Explanation 1
```

d'a'B'c'd ---> 'd'ABC'd' ---> ABC
 'a','c'        'd','d'
```

We have `a = daBcd` and  `b=ABC`. We perform the following operation:

Capitalize the letters `a` and `c` in `a` so that `a = dABCd`.
Delete all the remaining lowercase letters in `a` so that `a = ABC`.
Because we were able to successfully convert `a` to `b`, we print YES on a new line.

## Code

```python
 #!/bin/python3

import math
import os
import random
import re
import sys
    
# Complete the abbreviation function below.
def abbreviation(a, b):
    """
    문자열 a, b가 주어질때 a를 b와 동일하게 만들 수 있는지 검사
    대신, 아래 조건만 가능
        - a의 소문자를 대문자로 변경
        - a의 남은 소문자를 삭제
    """
    m, n = len(a), len(b)
    dp = [[False]*(m+1) for _ in range(n+1)]
    dp[0][0] = True
    print(dp)
    for i in range(n+1):
        for j in range(m+1):
            if i == 0 and j != 0:
                dp[i][j] = a[j-1].islower() and dp[i][j-1]
            elif i != 0 and j != 0:
                if a[j-1] == b[i-1]:
                    dp[i][j] = dp[i-1][j-1]
                elif a[j-1].upper() == b[i-1]:
                    dp[i][j] = dp[i-1][j-1] or dp[i][j-1]
                elif not (a[j-1].isupper() and b[i-1].isupper()):
                    dp[i][j] = dp[i][j-1]
    return "YES" if dp[n][m] else "NO"


if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # q = int(input())

    # for q_itr in range(q):
        # a = input()

        # b = input()

        # result = abbreviation(a, b)
        result = abbreviation("daBcd", "ABC")

        # fptr.write(result + '\n')

    # fptr.close()
```
