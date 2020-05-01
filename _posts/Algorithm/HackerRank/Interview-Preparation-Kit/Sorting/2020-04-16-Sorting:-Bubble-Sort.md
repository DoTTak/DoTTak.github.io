---
layout: post
title: "[Algorithm/HackerRank] Sorting - Sorting: Bubble Sort"
date: 2020-04-16 01:59:34 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Sorting
toc: true
---

<!-- more -->


## Probleam
Consider the following version of Bubble Sort:
```
java
for (int i = 0; i < n; i++) {
    
    for (int j = 0; j < n - 1; j++) {
        // Swap adjacent elements if they are in decreasing order
        if (a[j] > a[j + 1]) {
            swap(a[j], a[j + 1]);
        }
    }
    
}
```

Given an array of integers, sort the array in ascending order using the Bubble Sort algorithm above. Once sorted, print the following three lines:

1. Array is sorted in numSwaps swaps., where `numSwaps` is the number of swaps that took place.
2. First Element: firstElement, where `firstElement`` is the first element in the sorted array.
3. Last Element: lastElement, where `lastElement` is the last element in the sorted array.
**Hint:** To complete this challenge, you must add a variable that keeps a running tally of all swaps that occur during execution.

For example, given a worst-case but small array to sort: `a=[6, 4, 1]` we go through the following steps:
```

swap    a       
0       [6,4,1]
1       [4,6,1]
2       [4,1,6]
3       [1,4,6]
```

It took `3` swaps to sort the array. Output would be
```

Array is sorted in 3 swaps.  
First Element: 1  
Last Element: 6  
```


## Function Description
Complete the function countSwaps in the editor below. It should print the three lines required, then return.

countSwaps has the following parameter(s):

- a: an array of integers .

## Input Format
The first line contains an integer, `n`, the size of the array `a`.
The second line contains `n` space-separated integers `a[i]`.

## Output Format
You must print the following three lines of output:

1. Array is sorted in numSwaps swaps., where `numSwaps` is the number of swaps that took place.
2. First Element: firstElement, where `firstElement` is the first element in the sorted array.
3. Last Element: lastElement, where `lastElement` is the last element in the sorted array.

## Sample Input 1
```

3
1 2 3
```


## Sample Output 1
```

Array is sorted in 0 swaps.
First Element: 1
Last Element: 3
```


## Sample Input 2
```

3
3 2 1
```


## Sample Output 2
```

Array is sorted in 3 swaps.
First Element: 1
Last Element: 3
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the countSwaps function below.
def countSwaps(a):
    swap = 0

    for i in range(len(a)):       
        for j in range(len(a)-1): # Bubble Sorting은 원소를 끝으로 보내므로 1회는 빼줌
            if a[j] > a[j+1]:
                a[j], a[j+1] = a[j+1], a[j]
                swap += 1
    
    print("Array is sorted in %d swaps." % swap)
    print("First Element: %d" % a[0])
    print("Last Element: %d" % a[-1])

if __name__ == '__main__':
    # n = int(input())

    # a = list(map(int, input().rstrip().split()))

    countSwaps([3, 2, 1])
```
