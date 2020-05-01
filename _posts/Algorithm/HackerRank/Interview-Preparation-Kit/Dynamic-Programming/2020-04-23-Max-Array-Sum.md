---
layout: post
title: "[Algorithm/HackerRank] Dynamic Programming - Max Array Sum"
date: 2020-04-23 06:15:49 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Dynamic Programming
---

<!-- more -->


## Probleam
Given an array of integers, find the subset of non-adjacent elements with the maximum sum. Calculate the sum of that subset.

For example, given an array `arr = [-2, 1, 3, -4, 5]` we have the following possible subsets:
```
Subset      Sum
[-2, 3, 5]   6
[-2, 3]      1
[-2, -4]    -6
[-2, 5]      3
[1, -4]     -3
[1, 5]       6
[3, 5]       8
```

Our maximum subset sum is `8`.

## Function Description
Complete the `maxSubsetSum` function in the editor below. It should return an integer representing the maximum subset sum for the given array.

maxSubsetSum has the following parameter(s):
- arr: an array of integers

## Input Format
The first line contains an integer, `n`.
The second line contains `n` space-separated integers `arr[i]`.

## Output Format
Return the maximum sum described in the statement.

## Sample Input 1
```
5
3 7 4 6 5
```


## Sample Output 1
```
13
```


## Explanation 1
Our possible subsets are `[3,4,5], [3,4], [3,6], [3,5], [7,6], [7,5]` and `[4,5]`. The largest subset sum is `13` from subset `[7,6]`

## Code

```python
 #!/bin/python3

import math
import os
import random
import re
import sys

# Complete the maxSubsetSum function below.
def maxSubsetSum(arr):
    """
    arr에서 subarry중 요소가 인접되지 않은 경우의 집합의 합 중 제일 큰 값
    ex) arr = [-2, 1, 3, -4, 5] 의 비인접(인접되지 않음) SubArray는 ?
        [-2], [1], [3], [-4], [5]
        [-2,3], [-2,-4], [-2,5]
        [1,-4], [1,5]
        [3,5]
        [-2,3,5] 이다.    
    1. DP를 이용해서 풀자
    2. dp배열의 첫 번째, 두 번째 요소는 수동으로 구함
        2-1. dp[0]은 subarry의 첫 번째 요소와 0을 비교
        2-2. dp[1]은 dp[0]과 subarray의 두 번째 요소를 비교
    3. dp[2] 부터는 비교할 대상이 총 세가지이다. 이중 제일 큰 값
        3-1. subarray의 세 번째 요소(첫 번째, 두 번째는 위의 2-1,2-2에서 구했기 때문)
            - 세 번째 요소 이후로 반복해야함.(즉, i는 2부터 시작) -> arr[i]
        3-2. dp에서 현재 위치의 바로 이전과 비교(i-1) -> dp[i-1]
        3-3. 비인접행렬이므로 dp에서 -2를 한 위치와 자기자신을 더했을 경우 -> dp[i-2]+arr[i]
            - 예를들어 [a,b,c,d,e] 배열이 주어질 때 현재 반복문의 위치가 c인경우 
              a와 c 즉, 비인접 상태에서의 최댓값을 구해야 하므로 a와 c를 더하는 거라고 보면 됨.
                c가 arr[i]이고 -> 3-1에 의해 세 번째 요소 이후로 반복되므로 첫번째 순환에서는 값이 2임(0, 1, 2)
                a가 dp[i-2]라고 보면됨  -> a의 순서는 이미 2-1 즉, 첫번 째 요소를 비교한 최댓값이므로.
    """
    if len(arr) == 1:
        return arr[0]

    dp = []
    dp.append(max(0, arr[0]))
    dp.append(max(dp[0], arr[1]))
    dp = dp + [0]*(len(arr)-2)
    for i in range(2, len(arr)):
        dp[i] = max(arr[i], dp[i-1], dp[i-2]+arr[i])
    print(dp)
    return dp[-1]

    

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # n = int(input())

    # arr = list(map(int, input().rstrip().split()))

    # res = maxSubsetSum(arr)
    # res = maxSubsetSum([3, 7, 4, 6, 5])
    # res = maxSubsetSum([2, 1, 5, 8, 4])
    # res = maxSubsetSum([3, 5, -7, 8, 10])
    res = maxSubsetSum([3, -5, -7, -8, 10])
    # res = maxSubsetSum([1, 3, 10, 1])

    # fptr.write(str(res) + '\n')

    # fptr.close()

```
