---
layout: post
title: "[Algorithm/HackerRank] Arrays - Left Rotation"
date: 2020-04-16 01:36:29 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Arrays
toc: true
---

<!-- more -->


## Probleam
A left rotation operation on an array shifts each of the array's elements `1` unit to the left. For example, if `2` left rotations are performed on array `[1, 2, 3, 4, 5]`, then the array would become `[3, 4, 5, 1, 2]`.

Given an array `a` of `n` integers and a number, `d`, perform `d` left rotations on the array. Return the updated array to be printed as a single line of space-separated integers.

## Function Description
Complete the function rotLeft in the editor below. It should return the resulting array of integers.

rotLeft has the following parameter(s):

- An array of integers `a`.
- An integer `d`, the number of rotations.

## Input Format
The first line contains two space-separated integers `n` and `s`, the size of `a` and the number of left rotations you must perform.
The second line contains `n` space-separated integers `a[i]`.

## Output Format
Print a single line of `n` space-separated integers denoting the final state of the array after performing `d` left rotations.


## Sample Input 1
```

5 4
1 2 3 4 5
```


## Sample Output 1
```

5 1 2 3 4
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the rotLeft function below.
def rotLeft(a, d):
    for i in range(d):
        
        pull_num = a[0]

        del a[0]

        a.append(pull_num)
    
    return a

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nd = input().split()

    n = int(nd[0])

    d = int(nd[1])

    a = list(map(int, input().rstrip().split()))

    result = rotLeft(a, d)
    print(' '.join(map(str, result)))

    # fptr.write(' '.join(map(str, result)))
    # fptr.write('\n')

    # fptr.close()

```
