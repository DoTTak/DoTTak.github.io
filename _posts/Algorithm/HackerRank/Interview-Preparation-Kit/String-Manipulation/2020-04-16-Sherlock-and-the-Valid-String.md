---
layout: post
title: "[Algorithm/HackerRank] String Manipulation - Sherlock and the Valid String"
date: 2020-04-16 02:23:53 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - String Manipulation
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->

Sherlock considers a string to be valid if all characters of the string appear the same number of times. It is also valid if he can remove just `1` character at `1` index in the string, and the remaining characters will occur the same number of times. Given a string `s`, determine if it is valid. If so, return YES, otherwise return NO.

For example, if `s = abc`, it is a valid string because frequencies are `{a: 1, b:1, c:1}`. So is `s = abcc` because we can remove one `c` and have `1` of each character in the remaining string. If `s = abccc` however, the string is not valid as we can only remove `1` occurrence of . That would leave character frequencies of `{a:1, b:1, c:2}`.

## Function Description
Complete the isValid function in the editor below. It should return either the string YES or the string NO.

isValid has the following parameter(s):
- s: a string

## Input Format
A single string `s`.

## Output Format
Print YES if string `s` is valid, otherwise, print NO.

## Sample Input 1
```

aabbccddeefghi
```


## Sample Output 1
```

NO
```


## Sample Input 2
```

abcdefghhgfedecba
```


## Sample Output 2
```

YES
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the isValid function below.
def isValid(s):
    
    string_dict = {}
    find_dict = {}

    for i in range(len(s)):
        if s[i] in string_dict.keys():
            string_dict[s[i]] += 1
        else:
            string_dict[s[i]] = 1
    
    for k in string_dict.keys():
        if string_dict[k] in find_dict:
            find_dict[string_dict[k]] += 1
        else:
            find_dict[string_dict[k]] = 1

    print(string_dict)
    print(find_dict)

    if len(find_dict.keys()) > 2:
        return "NO"

    key =  list(find_dict.keys())[0]
    val = find_dict[key]
    for i in find_dict.keys():
       
        if i != key and find_dict[i] != 1:
            return "NO" 
    
    return "YES"


if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # s = input()

    # result = isValid("aabbccddeefghi")
    result = isValid("abcdefghhgfedecba")
    print(result)
    # fptr.write(result + '\n')

    # fptr.close()
```
