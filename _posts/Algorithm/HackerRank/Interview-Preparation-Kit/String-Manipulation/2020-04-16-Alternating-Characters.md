---
layout: post
title: "[Algorithm/HackerRank] String Manipulation - Alternating Characters"
date: 2020-04-16 02:23:53 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - String Manipulation
---

<!-- more -->


## Probleam
You are given a string containing characters `A` and `B` only. Your task is to change it into a string such that there are no matching adjacent characters. To do this, you are allowed to delete zero or more characters in the string.

Your task is to find the minimum number of required deletions.

For example, given the string `s = AABAAB`, remove an `A` at positions `0` and `3` to make `s = ABAB` in `2` deletions.

## Function Description
Complete the alternatingCharacters function in the editor below. It must return an integer representing the minimum number of deletions to make the alternating string.

alternatingCharacters has the following parameter(s):
- s: a string

## Input Format
The first line contains an integer `q`, the number of queries.
The next `q` lines each contain a string `s`.

## Output Format
For each query, print the minimum number of deletions required on a new line.

## Sample Input 1
```

5
AAAA
BBBBB
ABABABAB
BABABA
AAABBB
```


## Sample Output 1
```

3
4
0
0
4
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the alternatingCharacters function below.
def alternatingCharacters(s):
    start_s = s[0]
    count = 0
    
    for i in range(len(s)-1):
        if s[i+1] == start_s:
            count +=1
        else:
            start_s = s[i+1]
    
    return count

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s = input()

        result = alternatingCharacters(s)

        fptr.write(str(result) + '\n')

    fptr.close()

```
