---
layout: post
title: "[Algorithm/HackerRank] String Manipulation - Making Anagrams"
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
Alice is taking a cryptography class and finding anagrams to be very useful. We consider two strings to be anagrams of each other if the first string's letters can be rearranged to form the second string. In other words, both strings must contain the same exact letters in the same exact frequency For example, bacdc and dcbac are anagrams, but bacdc and dcbad are not.

Alice decides on an encryption scheme involving two large strings where encryption is dependent on the minimum number of character deletions required to make the two strings anagrams. Can you help her find this number?

Given two strings, `a` and `b`, that may or may not be of the same length, determine the minimum number of character deletions required to make `a` and `b` anagrams. Any characters can be deleted from either of the strings.

For example, if `a = cde` and `b = dcf`, we can delete `e` from string `a` and `f` from string `b` so that both remaining strings are `cd` and `dc` which are anagrams.

## Function Description
Complete the makeAnagram function in the editor below. It must return an integer representing the minimum total characters that must be deleted to make the strings anagrams.

makeAnagram has the following parameter(s):
- a: a string
- b: a string

## Input Format
The first line contains a single string, `a`.
The second line contains a single string, `b`.

## Output Format
Print a single integer denoting the number of characters you must delete to make the two strings anagrams of each other.



### Sample Input 1
```

cde
abc
```


### Sample Output 1
```

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

# Complete the makeAnagram function below.
def makeAnagram(a, b):
    string_a_dict = {}
    string_b_dict = {}
    count = 0

    # Strings A to Dict
    for i in a:
        if i in string_a_dict.keys():
            string_a_dict[i] += 1
        else:
            string_a_dict[i] = 1
    
    for i in b:
        if i in string_b_dict.keys():
            string_b_dict[i] += 1
        else:
            string_b_dict[i] = 1

    for k in string_a_dict.keys():
        if k in string_b_dict.keys():
            if string_a_dict[k] > string_b_dict[k]:
                count += string_a_dict[k] - string_b_dict[k]
            else:
                count += string_b_dict[k] - string_a_dict[k]
        else:
            count += string_a_dict[k]
    
    for k in string_b_dict.keys():
        if not k in string_a_dict.keys():
            count += string_b_dict[k]
            
    return count

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # a = input()

    # b = input()

    # res = makeAnagram(a, b)
    res = makeAnagram("cde", "abc")

    # fptr.write(str(res) + '\n')

    # fptr.close()

```
