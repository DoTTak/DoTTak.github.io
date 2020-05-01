---
layout: post
title: "[Algorithm/HackerRank] String Manipulation - Common Child"
date: 2020-04-16 02:23:53 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - String Manipulation
toc: true
---

<!-- more -->


## Probleam
A string is said to be a child of a another string if it can be formed by deleting 0 or more characters from the other string. Given two strings of equal length, what's the longest string that can be constructed such that it is a child of both?

For example, ABCD and ABDC have two children with maximum length 3, ABC and ABD. They can be formed by eliminating either the D or C from both strings. Note that we will not consider ABCD as a common child because we can't rearrange characters and ABCD \neq ABDC.

## Function Description

Complete the commonChild function in the editor below. It should return the longest string which is a common child of the input strings.

commonChild has the following parameter(s):
- s1, s2: two equal length strings

## Input Format
There is one line with two space-separated strings, `s1` and `s2`.

## Output Format
Print the length of the longest string `s`, such that `s` is a child of both `s1` and `s2`.

## Sample Input 1
```

HARRY
SALLY
```


## Sample Output 1
```

2
```


## Sample Input 2
```

AA
BB
```


## Sample Output 2
```

0
```


## Sample Input 3
```

SHINCHAN
NOHARAAA
```


## Sample Output 3
```

33
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the commonChild function below.
def commonChild(s1, s2):

    # Matrix 만들기
    row_size = len(s1) + 1
    col_size = len(s2) + 1

    matrix = []
    for i in range(row_size):
        row = []
        for j in range(col_size):
            row.append(0)
        matrix.append(row)
    
    # LCS 길이구하기
    # 첫번째 행,열은 0으로 구분해야하므로 1부터 시작
    for i in range(1, row_size):
        for j in range(1, col_size):
            if s1[i-1] == s2[j-1]:
                # 같은경우 대각선 +1
                matrix[i][j] = matrix[i-1][j-1] + 1
            else:
                # 다른경우 왼쪽 OR 위쪽에서 큰 값 
                matrix[i][j] = max(matrix[i-1][j], matrix[i][j-1])
        
    # LCS의 길이는?
    return matrix[-1][-1]

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # s1 = input()

    # s2 = input()

    # result = commonChild("SHINCHAN", "NOHARAAA")
    result = commonChild("OUDFRMYMAW", "AWHYFCCMQX")
    print(result)
    # fptr.write(str(result) + '\n')

    # fptr.close()
```
