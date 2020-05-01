---
layout: post
title: "[Algorithm/HackerRank] Dictionaries and Hashmaps - Two Strings"
date: 2020-04-16 01:47:33 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Dictionaries and Hashmaps
---

<!-- more -->


## Probleam
Given two strings, determine if they share a common substring. A substring may be as small as one character.

For example, the words "a", "and", "art" share the common substring . The words "be" and "cat" do not share a substring.

## Function Description

Complete the function twoStrings in the editor below. It should return a string, either YES or NO based on whether the strings share a common substring.

twoStrings has the following parameter(s):
- s1, s2: two strings to analyze .

## Input Format
The first line contains a single integer `p`, the number of test cases.

The following `p` pairs of lines are as follows:
- The first line contains string `s1`.
- The second line contains string `s1`.

## Output Format
For each pair of strings, return YES or NO.

## Sample Input 1
```

2
hello
world
hi
world
```


## Sample Output 1
```

YES
NO
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the twoStrings function below.
def twoStrings(s1, s2):
    string_dict = {}

    for i in s1:
        if i in string_dict.keys():
            string_dict[i] += 1
        else:
            string_dict[i] = 1
    
    is_pair = False
    for i in s2:
        if i in string_dict.keys():
            is_pair = True
            break
    
    if not is_pair:
        return "NO"
    else:
        return "YES"

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s1 = input()

        s2 = input()

        result = twoStrings(s1, s2)

    #     fptr.write(result + '\n')

    # fptr.close()
```
