---
layout: post
title: "[Algorithm/HackerRank] Dictionaries and Hashmaps - Sherlock and Anagrams"
date: 2020-04-16 01:49:30 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Dictionaries and Hashmaps
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
Two strings are anagrams of each other if the letters of one string can be rearranged to form the other string. Given a string, find the number of pairs of substrings of the string that are anagrams of each other.

For example `s=mom`, the list of all anagrammatic pairs is `[m,m], [mo,om]` at positions `[[0], [2]], [[0,1],[1,2]]` respectively.

## Function Description

Complete the function sherlockAndAnagrams in the editor below. It must return an integer that represents the number of anagrammatic pairs of substrings in `s`.

sherlockAndAnagrams has the following parameter(s):
- s: a string .

## Input Format
The first line contains an integer `q`, the number of queries.
Each of the next `q` lines contains a string `s` to analyze.

## Output Format
For each query, return the number of unordered anagrammatic pairs.

## Sample Input 1
```

2
abba
abcd
```


## Sample Output 1
```

4
0
```


## Sample Input 1
```

2
ifailuhkqq
kkkk
```


## Sample Output 1
```

3
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

# Complete the sherlockAndAnagrams function below.
def sherlockAndAnagrams(s):
    total = 0
    answer_dict = {}
    """
    주어진 s에서 substring으로 빼낼 수 있는 단어의 갯수 구하기
    [참고]
    아래 예시의 "kkkk"의 경우 한자리가 전부 같은 "k"일 때
    같은 k라도 위치에 따라 다른 k이다.
    ex) "kkkk"
    k       [0:1]   [1:2]   [2:3]   [3:4]
            (k)kkk  k(k)kk  kk(k)k  kkk(k)
    kk      [0:2]   [1:3]   [2:4]
            (kk)kk  k(kk)k  kk(kk)
    kkk     [0:3]   [1:4]
            (kkk)k  k(kkk)
    kkkk    [0:4]
            (kkkk)
    substring k, kk, kkk, kkkk가 각각 4, 3, 2, 1개로 나오지만 위치마다
    다른 단어이므로 총 kkkk에서 나오는단어는 4+3+2+1 = 10이다.
    하지만 짝을 찾는 경우 kkkk는 "kkkk"문자에서 짝을 지을 수 없기에 제외
    대신, k, kk, kkk는 짝을 찾을 수 있다.
    [k의 짝이 이루어지는 경우]
       [k...]와[.k..]
       [k...]와[..k.]
       [k...]와[...k]
       [.k..]와[..k.]         k 총 6개
       [.k..]와[...k]
       [..k.]와[..kk]
    [kk의 짝이 이루어지는 경우]
        [kk..]와 [..kk]
        [kk..]와 [.kk.]      kk 총 3개
        [.kk.]와 [..kk]
    [kkk의 짝이 일워지는 경우]
        [kkk.]와 [.kkk]     kkk 총 1개

    k 총 갯수 + kk 총 갯수 + kkk 총 갯수 = 10개
    공식은 n*(n-1)//2  -> k의경우 4*(4-1)//2 = 6
        -> n은 똑같은 글자가 발견된 갯수
    """
    for i in range(len(s)):
        for j in range(i+1, len(s)+1):
            sorted_letter = ''.join(sorted(s[i:j]))
            print(sorted_letter)
            answer_dict.setdefault(sorted_letter, 0)
            answer_dict[sorted_letter] += 1

    for i in answer_dict.values():
        total += i*(i-1)//2

    return total

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s = input()

        result = sherlockAndAnagrams(s)

        # fptr.write(str(result) + '\n')

    # fptr.close()

```
