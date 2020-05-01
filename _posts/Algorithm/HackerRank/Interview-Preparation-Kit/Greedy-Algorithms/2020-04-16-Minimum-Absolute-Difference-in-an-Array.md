---
layout: post
title: "[Algorithm/HackerRank] Greedy Algorithms - Minimum Absolute Difference in an Array"
date: 2020-04-16 02:27:58 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Greedy Algorithms
---

<!-- more -->


## Probleam
Consider an array of integers, `arr = [arr[0], arr[1], ..., arr[n-1]]`. We define the absolute difference between two elements, `a[i]` and `a[j]`(where `i`\neq`j`), to be the absolute value of `a[i] - a[j]`.

Given an array of integers, find and print the minimum absolute difference between any two elements in the array. For example, given the array `arr = [-2, 2, 4]` we can create `3` pairs of numbers: `[-2,2],[-2,4]` and `[2,4]`. The absolute differences for these pairs are `|(-2)-2| = 4`, `|(-2)-4|=6` and `|2-4|=2`. The minimum absolute difference is `2`.

## Function Description
Complete the minimumAbsoluteDifference function in the editor below. It should return an integer that represents the minimum absolute difference between any pair of elements.

minimumAbsoluteDifference has the following parameter(s):
- n: an integer that represents the length of arr
- arr: an array of integers

## Input Format
The first line contains a single integer `n`, the size of `arr`.
The second line contains `n` space-separated integers `arr[i]`.

## Output Format
Print the minimum absolute difference between any two elements in the array.

## Sample Input 1
```

3
3 -7 0
```


## Sample Output 1
```

3
```


## Sample Input 2
```

10
-59 -36 -13 1 -53 -92 -2 -96 -54 75
```


## Sample Output 2
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

# Complete the minimumAbsoluteDifference function below.
def minimumAbsoluteDifference(arr):

	"""
	TimeOut 
	"""
	# for i in range(0, len(arr)-1):
	# 	for j in range(i+1,len(arr)):
	# 		absolute_num = abs(arr[i] - arr[j])
	# 		if minimum != None:
	# 			if minimum > absolute_num:
	# 				minimum = absolute_num
	# 		else:
	# 			minimum = absolute_num
	
	diff_arr = []
	sort_arr = sorted(arr)
	for i in range(0, len(sort_arr)-1):
		diff_arr.append(abs(sort_arr[i] - sort_arr[i+1]))
	

	return min(diff_arr)

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # n = int(input())

    # arr = list(map(int, input().rstrip().split()))

    result = minimumAbsoluteDifference([-59,-36,-13,1,-53,-92,-2,-96,-54,75])

    # fptr.write(str(result) + '\n')

    # fptr.close()

```
