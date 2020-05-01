---
layout: post
title: "[Algorithm/HackerRank] Warm_up Challenges - Repeated String"
date: 2020-04-16 01:24:58 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Warm_up Challenges
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
Lilah has a string, `s`, of lowercase English letters that she repeated infinitely many times.

Given an integer, `n`, find and print the number of letter a's in the first  letters of Lilah's infinite string.

For example, if the string `s='abcac'` and `n=10`, the substring we consider is `abcacabcac`, the first `10` characters of her infinite string. There are `4` occurrences of a in the substring.

## Function Description
Complete the repeatedString function in the editor below. It should return an integer representing the number of occurrences of a in the prefix of length  in the infinitely repeating string.

repeatedString has the following parameter(s):

- s: a string to repeat
- n: the number of characters to consider

# Input Format
The first line contains a single string, `s`.
The second line contains an integer, `n`.

## Output Format
Print a single integer denoting the number of letter a's in the first `n` letters of the infinite string created by repeating `s` infinitely many times.

## Sample Input 1
```

aba
10
```


## Sample Output 1
```

7
```


## Sample Input 2
```

a
1000000000000
```


## Sample Output 2
```

1000000000000
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the repeatedString function below.
def repeatedString(s, n):
	word_len = len(s) # 입력받은 문자열의 길이
	a_of_word = s.count('a')
	result = 0

	# 입력받은 n 길이만큼 s의 문자열을 만든다면
	mok = int(n / word_len)
	nmg = n % word_len

	result = (mok * a_of_word) + s[0:nmg].count('a')
	
	return result

if __name__ == '__main__':
	# fptr = open(os.environ['OUTPUT_PATH'], 'w')

	s = input()

	n = int(input())

	result = repeatedString(s, n)

	print(result)
	# fptr.write(str(result) + '\n')

	# fptr.close()

```
