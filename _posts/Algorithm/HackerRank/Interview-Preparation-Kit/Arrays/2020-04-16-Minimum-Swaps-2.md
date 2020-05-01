---
layout: post
title: "[Algorithm/HackerRank] Arrays - Minimum Swaps 2"
date: 2020-04-16 01:41:38 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Arrays
---

<!-- more -->


## Probleam
You are given an unordered array consisting of consecutive integers \in [1, 2, 3, ..., n] without any duplicates. You are allowed to swap any two elements. You need to find the minimum number of swaps required to sort the array in ascending order.

For example, given the array `arr=[7, 1, 3, 2, 4, 5, 6]` we perform the following steps:
```

i   arr                         swap (indices)
0   [7, 1, 3, 2, 4, 5, 6]   swap (0,3)
1   [2, 1, 3, 7, 4, 5, 6]   swap (0,1)
2   [1, 2, 3, 7, 4, 5, 6]   swap (3,4)
3   [1, 2, 3, 4, 7, 5, 6]   swap (4,5)
4   [1, 2, 3, 4, 5, 7, 6]   swap (5,6)
5   [1, 2, 3, 4, 5, 6, 7]
```

It took `5` swaps to sort the array.

## Function Description
Complete the function minimumSwaps in the editor below. It must return an integer representing the minimum number of swaps to sort the array.

minimumSwaps has the following parameter(s):

- arr: an unordered array of integers

## Input Format
The first line contains an integer, `n`, the size of `arr`.
The second line contains `n` space-separated integers `arr[i]`.

## Output Format
Return the minimum number of swaps to sort the given array.

## Sample Input 1
```

5
2 3 4 1 5
```


## Sample Output 1
```

3
```


## Sample Input 2
```

7
1 3 5 2 4 6 7
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

# Complete the minimumSwaps function below.
def minimumSwaps(arr):
    # 최소 선택 알고리즘은 선택정렬
    swap_count = 0
    for i in range(len(arr)):
        
        while arr[i] != i+1:
            temp = arr[i]
            arr[i] = arr[temp-1]
            arr[temp-1] = temp        # 실제 정렬이 올바르게 되는 부분
            
            swap_count += 1

    return swap_count
    
if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    arr = list(map(int, input().rstrip().split()))

    res = minimumSwaps(arr)
    print(res)
    # fptr.write(str(res) + '\n')

    # fptr.close()

```
