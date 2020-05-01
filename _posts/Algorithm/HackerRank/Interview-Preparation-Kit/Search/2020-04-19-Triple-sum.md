---
layout: post
title: "[Algorithm/HackerRank] Search - Triple sum"
date: 2020-04-19 08:26:07 +0900
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
Given `3` arrays `a, b, c` of different sizes, find the number of distinct triplets `(p, q, r)` where `q` is an element of `a`, written as `p \in a`, `q \in b`, and `r \in c`, satisfying the criteria: `p <= q and q >= r`.

For example, given `a = [3, 5, 7], b = [3, 6]` and `c = [4, 6, 9]`, we find four distinct triplets: `(3,6,4), (3,6,6), (5,6,4), (5,6,6)`.

## Function Description
Complete the triplets function in the editor below. It must return the number of distinct triplets that can be formed from the given arrays.

triplets has the following parameter(s):
- a, b, c: three arrays of integers .

## Input Format
The first line contains `3` integers `lena, lenb, and lenc`, the sizes of the three arrays.
The next `3` lines contain space-separated integers numbering `lena, lenb, and lenc` respectively.

## Output Format
Print an integer representing the number of distinct triplets.

## Sample Input 1
```

3 2 3
1 3 5
2 3
1 2 3
```


## Sample Output 1
```

8
```


## Explanation 1
The special triplets are 
`(1,2,1), (1,2,2), (1,3,1), (1,3,2), (1,3,3), (3,3,1), (3,3,2), (3,3,3)`

## Code

```python
 #!/bin/python3

import math
import os
import random
import re
import sys

# Complete the triplets function below.
def triplets(a, b, c):
    """
    배열 a, b, c가 주어질때 각 배열의 요소를 하나씩 뽑아내서 (p, q, r)을 만들 때
    만들 수 있는 총 조합의 수를 구하기.
    - 조건 
        - (p는 a의 요소, q는 b의 요소, r은 c의 요소)
        - p는 q보다 작거나 같다. AND q는 r보다 크거나 같다.
        - 중복은 없다.
    """

    # Solution 1            -> Timeout -> O(n^3)
    # count = 0
    # temp = []
    # for i1 in range(0, len(a)):
    #     for i2 in range(0, len(b)):
    #         for i3 in range(0, len(c)):
    #             p = a[i1]
    #             q = b[i2]
    #             r = c[i3]
    #             print(count)
    #             if p <= q and q >= r:
    #                 if not [p,q,r] in temp:
    #                     temp.append([p,q,r])
    #                     print(p, q, r)
    #                     count +=1 
    # return count


    # Solution 2
   
    # 요소에서 중복되는거는 삭제하고 정렬
    a = list(sorted(set(a)))    
    b = list(sorted(set(b)))  
    c = list(sorted(set(c)))
    
    ai = 0
    bi = 0
    ci = 0
    
    ans = 0
    
    """
    위에서 각 a, b, c의 배열을 정렬 했을 때 특징은
    기준이 되는 값 b 리스트 보다 작은 값이 앞, 뒤 리스트에 존재하고
    마지막 인덱스에 도달하면 b 리스트의 나머지 값들은 자동으로 큰 값으로 설정된다.
    그래서 앞, 뒤 리스트를 순회하면서 해당 인덱스를 저장 하면 순회횟수가 줄어듬
    -> 아래 조건을 이용
        - (p는 a의 요소, q는 b의 요소, r은 c의 요소)
        - p는 q보다 작거나 같다. AND q는 r보다 크거나 같다.

    """
    while bi < len(b):
        while ai < len(a) and a[ai] <= b[bi]:
            ai += 1
        
        while ci < len(c) and c[ci] <= b[bi]:
            ci += 1
        
        ans += ai * ci
        bi += 1
    
    return ans

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # lenaLenbLenc = input().split()

    # lena = int(lenaLenbLenc[0])

    # lenb = int(lenaLenbLenc[1])

    # lenc = int(lenaLenbLenc[2])

    # arra = list(map(int, input().rstrip().split()))

    # arrb = list(map(int, input().rstrip().split()))

    # arrc = list(map(int, input().rstrip().split()))

    # ans = triplets([1,3,5], [2,3], [1,2,3])
    ans = triplets([1,4,5], [2,3,3], [1,2,3])

    # fptr.write(str(ans) + '\n')

    # fptr.close()

```
