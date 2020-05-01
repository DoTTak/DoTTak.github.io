---
layout: post
title: "[Algorithm/HackerRank] Search - Maximum Subarray Sum"
date: 2020-04-21 10:19:56 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Search
---

<!-- more -->


## Probleam
We define the following:
- A subarray of array  of length  is a contiguous segment from  through  where .
- The sum of an array is the sum of its elements.

Given an `n` element array of integers, `a`, and an integer, `m`, determine the maximum value of the sum of any of its subarrays modulo `m`. For example, Assume `a=[1,2,3]` and `m=2`. The following table lists all subarrays and their moduli:
```

		    sum	%2
[1]		    1	1
[2]		    2	0
[3]		    3	1
[1,2]		3	1
[2,3]		5	1
[1,2,3]		6	0
```

The maximum modulus is `1`.

## Function Description
Complete the maximumSum function in the editor below. It should return a long integer that represents the maximum value of `subarray sum %m`.

maximumSum has the following parameter(s):
- a: an array of long integers, the array to analyze
- m: a long integer, the modulo divisor


## Input Format
The first line contains an integer `q`, the number of queries to perform.

The next `q` pairs of lines are as follows:

The first line contains two space-separated integers `n` and (long)`m`, the length of `a` and the modulo divisor.
The second line contains `n` space-separated long integers `a[i]`.

## Output Format
For each query, return the maximum value of `subarray sum % m` as a long integer.

## Sample Input 1
```

1
5 7
3 3 9 9 5
```


## Sample Output 1
```

6
```


## Explanation 1
The subarrays of array `a = [3,3,9,9,5]` and their respective sums modulo `m=7` are ranked in order of length and sum in the following list:
1. `[9] -> 9 % 7 = 2` and `[9] -> 9 % 7 = 2`<br>
    `[3] -> 3 % 7 = 3` and `[3] -> 3 % 7 = 3`<br>
    `[5] -> 5 % 7 =5`

2. `[9,5] -> 14 % 7 = 0`<br>
    `[9,9] -> 18 % 7 = 4`<br>
    `[3,9] -> 12 % 7 = 5`<br>
    `[3,3] -> 6 % 7 = 0`

3. `[3,9,9] -> 21 % 7 = 0`<br>
    `[3,3,9] -> 15 % 7 = 1`<br>
    `[9,9,5] -> 23 % 7 = 2`<br>

4. `[3,3,9,9] -> 24 % 7 = 3`<br>
    `[3,9,9,5] -> 26 % 7 = 5`<br>

5. `[3,3,9,9,5] -> 29 % 7 = 1`

The maximum value for `subarray sum % 7` for any subarray is `6`.

## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys
from bisect import *

# Complete the maximumSum function below.
def maximumSum(a, m):
    """
    1. 배열 a의 subarray를 구한다.  ex) [1,2,3] -> [1], [2], [3], [1,2], [1,3], [2,3]
    2. 해당 subarray의 요소를 합한다                 1    2    3    1+2     1+3   2+3
    3. 합친 subarray를 m으로 나눌때 나머지가 제일 큰 값을 구하면 됨.
        1, 2, 3, 3, 4, 5 에서 m이 3인 경우
        1%3 = 1
        2%3 = 2
        3%3 = 0 -> 답은 2
        3%3 = 0
        4%3 = 1
        5%3 = 2
    """

    """
    Solution 1  -> Timeout 발생
    """
    # max_num = 0
    # for i in range(0, len(a)-1):
    #     for j in range(i+1, len(a)):
    #         target = (a[i] + a[j]) % m
    #         if(target > max_num):
    #             max_num = target
    
    # return max_num

    """
    Solution 2

    먼저 문제는 각 subarray의 합에서 M을 나눌때 나머지 값 중 제일 큰 값을 찾는 것이다.
    예를들어 [7, 7, 1, 3]의 배열과 나머지 9가 주어질때,
    subarray는 
        [7], [7], [1], [3],
        [7.7], [7,1], [7,3]
        [7,1], [7,3]
        [1,3]
        [7,7,1], [7,7,3]
        [7,1,3]
        [7,7,1,3]
    각각의 요소들의 합은
        [7], [7], [1], [3],
        [14], [8], [10]
        [8], [10]
        [4]
        [15], [17]
        [11]
        [18]
    요소들의 합을 나누기 9를 한 후 나머지는
        [5], [8], [3]
        [8], [3]
        [4]
        [7], [1]
        [3]
        [0]
    이중 제일 큰 값이 8이므로 정답은 8이다.

    사실 이해하기 너무 어렵고 이해가 안됐다....
    다만 아래 공식으로 풀림
    """
    calculate_prefix = lambda cur, prev: (prev + (cur % m)) % m
    cur_prefix = calculate_prefix(a[0], 0)
    pq = [cur_prefix]
    maxmodsum = cur_prefix
    for i in range(1, len(a)):
        
        cur_prefix = calculate_prefix(a[i], cur_prefix)
        left = bisect_right(pq, cur_prefix)
        """
        prefix에 추가할 요소가 prefix 배열에 존재하는지 판단
        """
        if left != len(pq):
            # 배열에 존재하지 않을 경우
            """
            현재 prefix요소와 이전 prefix요소중 최댓값을 계산
            """
            modsum = max(cur_prefix, (cur_prefix - pq[left] + m) % m)
        else:
            # 배열에 존재 할 경우
            modsum = cur_prefix

        maxmodsum = max(maxmodsum, modsum)

        insort(pq, cur_prefix)
    return maxmodsum

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # q = int(input())

    # for q_itr in range(q):
    #     nm = input().split()

    #     n = int(nm[0])

    #     m = int(nm[1])

    #     a = list(map(int, input().rstrip().split()))

        # result = maximumSum(a, m)
        # result = maximumSum([1, 5, 9], 5)
        # result = maximumSum([3,3,9,9,5], 7)
        # print("---------")
        result = maximumSum([7,7,1,3], 9)

    #     fptr.write(str(result) + '\n')

    # fptr.close()
```
