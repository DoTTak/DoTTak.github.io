---
layout: post
title: "[Algorithm/HackerRank] Greedy Algorithms - Reverse Shuffle Merge"
date: 2020-04-16 02:44:06 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Greedy Algorithms
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
Given a string, `A`, we define some operations on the string as follows:

> a.`reverse(A)` denotes the string obtained by reversing string `A`. Example: `reverse("abc") = "cba"`
>
> b.`shuffle(A)` denotes any string that's a permutation of string `A`. Example: `shuffle("god")` \in `['god', 'gdo', 'ogd', 'odg', 'dgo', 'dog']`
>
> c.`merge(A1, A2)`  denotes any string that's obtained by interspersing the two strings `A1` & `A2`, maintaining the order of characters in both. For example, `A1 = 'abc'` & `A2 = 'def'`, one possible result of `merge(A1, A2)` could be `'abcdef'`, another could be `'abdecf'`, another could be `'adbecf'` and so on.

Given a string `s` such that `s` \in `merge(reverse(A), shuffle(A))` for some string `A`, find the lexicographically smallest `A`.

For example, `s = abab`. We can split it into two strings of `ab`. The reverse is `ba` and we need to find a string to shuffle in to get `abab`. The middle two characters match our reverse string, leaving the `a` and `b` at the ends. Our shuffle string needs to be `ab`. Lexicographically `ab < ba`, so our answer is `ab`.

## Function Description
Complete the reverseShuffleMerge function in the editor below. It must return the lexicographically smallest string fitting the criteria.

reverseShuffleMerge has the following parameter(s):
- s: a string

## Input Format
A single line containing the string .

## Output Format
Find and return the string which is the lexicographically smallest valid .


## Constraints

## Sample Input 1
```

eggegg
```


## Sample Output 1
```

egg
```


## Sample Input 2
```

abcdefgabcdefg
```


## Sample Output 2
```

agfedcb
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys
from collections import Counter
def reverseShuffleMerge(s):
    cnt = Counter(s)
    req = Counter({k:v // 2 for k,v in cnt.items()})
    rs = s[::-1]
    ic = ord('a')
    imax = ord('z') + 1
    pos = -1
    ans = ''
    while ic < imax:
        c = chr(ic)
        if c not in list(+req):
            ic += 1
            continue
        i = rs.find(c,pos + 1)
        if len(+(req - Counter(rs[i:]))) > 0:
            # not enough characters behind,find bigger character
            ic += 1
        else:
            # there are enough characters behind
            ans += c
            pos = i     #new position to find
            req[c] -= 1 #reduct request
            ic = ord('a')   #find from a to z
            if len(+req) == 0:  #find all
                return ans
        if ic >= imax:
            ic -= 26
    
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    s = input()

    result = reverseShuffleMerge(s)

    fptr.write(result + '\n')

    fptr.close()

```
