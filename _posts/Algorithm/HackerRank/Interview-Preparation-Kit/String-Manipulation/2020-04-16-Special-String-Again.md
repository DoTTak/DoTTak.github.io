---
layout: post
title: "[Algorithm/HackerRank] String Manipulation - Special String Again"
date: 2020-04-16 02:23:53 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - String Manipulation
toc: true
---

<!-- more -->


## Probleam
A string is said to be a special string if either of two conditions is met:

- All of the characters are the same, e.g. aaa.
- All characters except the middle one are the same, e.g. aadaa.
A special substring is any substring of a string which meets one of those criteria. Given a string, determine how many special substrings can be formed from it.

For example, given the string `s = mnonopoo`, we have the following special substrings: `{m, n, o, n, o, p, o, o, non, ono, opo, oo}`.

## Function Description
Complete the substrCount function in the editor below. It should return an integer representing the number of special substrings that can be formed from the given string.

substrCount has the following parameter(s):
- n: an integer, the length of string s
- s: a string

## Input Format
The first line contains an integer, `n`, the length of `s`.
The second line contains the string `s`.

## Output Format
Print a single line containing the count of total special substrings.

## Sample Input 1
```

5
asasd
```


## Sample Output 1
```

7
```


## Sample Input 2
```

7
abcbaba
```


## Sample Output 2
```

10
```


## Sample Input 3
```

4
aaaa
```


## Sample Output 3
```

10
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the substrCount function below.
def substrCount(n, s):
    """
    입력 string의 substring 중 palindromic string의 갯수
    palindromic string: 전체가 모두 같은 글자와 가운데 글자를 제외하고 모두 같은 글자

    [Example] aaaa, aabaa
    
    [풀이 1] 
    문자 aaaa는 (a,4) aabaa는 (a,2),(b,1),(a,2)로 표현 가능

    [풀이 2] 
    여기서 공식은 풀이 1의 각 자리수의 n(n+1)/2를 모두 합하면 갯수가 나온다.
    >> aaaa -> 4x(4+1)/2 == 10
        a, aa, aa, aa, a, aaa, aaa, a, aaaa, a
    >> aabaa -> 2x(2+1)/2 + 1x(1+1)/2 + 2x(2+1)/2 == 3 + 1 + 3 == 7
        a a aa b a aa a

    [풀이 2] 가운데 글자를 제외한 양 옆의 글자가 같은 글자의 수 구하기
    즉, [풀이 1]에서 갯수가 1인 양옆의 문자가 같은 경우를 찾으면 됨.
    aaaa 는 존재하지 않음
    aabaa는 (a,2),(b,1),(a,2) 에서 (b,1)을 기준으로 양 옆의 문자가 동일하다.
    단, 양옆의 글자중 작은 숫자를 골라야함. 즉, 답은 2(aabaa 는 aba와 aabaa가 있음)
    """

    # 풀이 1
    arr =[]
    cur = s[0]
    count = 1
    for i in range(1, n):
        if s[i] == cur:
            count +=1
        else:
            arr.append((s[i-1], count))
            cur = s[i]
            count = 1
    arr.append((cur, count))

    # 풀이 2
    answer = 0
    for i in arr:
        answer += (i[1]*(i[1]+1)) // 2

    # 풀이 3
    for i in range(1, len(arr)-1):
        if arr[i][1] == 1 and arr[i-1][0] == arr[i+1][0]:
            answer += min(arr[i-1][1], arr[i+1][1])

    return answer
    
if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # n = int(input())

    # s = input()

    # result = substrCount(4, "aaa]a")
    # result = substrCount(5, "asasd")
    result = substrCount(5, "aabaa")
    # result = substrCount(7, "abcbaba")
    print(result)
    # fptr.write(str(result) + '\n')

    # fptr.close()

```
